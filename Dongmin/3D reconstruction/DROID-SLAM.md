# DROID-SLAM: Deep Visual SLAM for Monocular, Stereo, and RGB-D Cameras (NeurIPS'21)

> Zachary Teed, Jia Deng

[Page Link](https://github.com/princeton-vl/DROID-SLAM)  

---
## System Overview
<img src="./assets/DROID-SLAM overview.png">

### Difference with prev works
1. DROID-SLAM uses dense BA layer, optimizes geometric reprojection error. 
- DeepV2D alternates between updating depth and camera poses, instead of BA
- DeepFactors and BA-Net is not 'dense' in that optimizes over a small number of coeff to linearly combine depth basis (a set of. re-predicted depth maps). Also, they optimizes over photometric reprojection error.   
 
2. Differntiable Recurrent Optimization-Inspired Design(DROID), which is an end-to-end differentiable architecture that combines the strengths of both classical approaches and deep networks. Building upon RAFT for optical flow with introducing two key innovations.
- RAFT iteratively updates optical flow, DROID-SLAM iteratively update camera poses and depth updates on arbitrary number of frames, enabling joint global refinement.
- Each update is produced by a differentiable Dense Bundle Adjustment (DBA) layer, which computes Gauss-Newton update to dense per-pixel depth to maximize estimate of optical flow. Enables a monocular system to handle stereo or RGB-D input without retraining.

3. Take inspirations from [Dusmanu et al](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460647.pdf), build neural network into the SfM pipeline to improve keypoint localization accuracy.

## Main structures
1. Adopt frame-graph to represent co-visibility between frames. An edge means an image I_i and I_j have overlapping fields of voew which shared points. The frame graph is build dynamically during training and inference. After every pose and depth update, recompute visibility to update frame graph. -> If the camera returns to previous position, make edge. 

2. Feature extraction is computed with 6 res block with 3 downsample layer results 1/8 resolution dense feature maps like RAFT. Uses two network, feature network used to build the set of correlation volumes, while context features are injected into the network during each update operator.
- Every edge, compute 4D correlation volume by taking the dot product by all pairs of feature vectors f(I_i), f(I_j), average pooling onn last two dim to form 4-level correlation pyramid
- Define lookup operator as RAFT takes an HxW grid of coordinates as input and values are retrieved from the correlation volume using bilinear interpolation, final feature vector is computed by concatenating the results at each level.
<img src="./assets/DROID Operator.png">.  
- Learning based operator acts on edges in frame graph, predict flow revision which are mapped to depth and pose update through th DBA layer
- 3x3 convolutional GRU updates pose and depth.
- Correspondence field p_ij is the coordinates of pixels p_i mapped in to frmae j using the estimated pose and depth. Use it to index correlation volume C_ij to retrieve correlation features, and optical flow p_ij-p_j
- If the correspondence in correlation features are ambiguous so that hard to align similar region, the flow provides an complementary information to explot smoothness in the motion.
- Correlation features and flow features are each mapped through two conv layer before injected into GRU, additionally inject context features from context network into the GRU through element-wise addition.
- ConvGRU is a local operation with small receptive field. Extract global context by averaging the hidden state across the spatial dim of the image and use it as additional input to GRU(global context).
- GRU updates in the space of dense flow fields rather than directly update pose and depth(hidden state update). Hidden states map through two addition conv layer to produce revison flow field r_ij and confidence map w_ij. 
- Dense Bundle Adjustment Layer (DBA) maps the set of flow revision s into a set of pose and pixelwise depth updates. Cost funtion is over the entire frame graph(geometric reprojection error) with conf w_ij Mahalanobis distance. For linearization, use local parameterization and use Gauss-Newton. Seperating pose and depth var, system can be solved dfficiently using the Schur complement.
- [RAFT video](https://youtu.be/OnZIDatotZ4) can help understanding

3. While training on mono setting, network only able to recover the trajectory of the camera up to a similarity transform. To handle this, define loss invariant to similarity transforms, and Gauge-freedom left. To manage it, fix the first two poses to the g.t pose of each training seq. fixing them removes the 6-dof gauge freedom. Fixing second pose resolves scale freedom.
- Each training vid consist of 7-frame video seq. For each video i of length N_i, precompute N_i x N_i distance matrix storing the average optical flow, and less than 50 % overlap are discarded. During training, dynamically generate videos by sampling paths in the distance matrix. (average flow between adjacent vid 8px to 96px)
- Supervise with pose loss and flow loss. (pose loss : L2 on T^-1_i dot G_i) : GT pose inv dot pred pose

---
### Improvements
1. Need proper initial guess which means if the sequential input frames differs a lot, it may fails on tracking. (network only able to recover the trajectory of the camera up to a similarity transform)

### Note
1. They use full image like direct method, allowing to leverage wider range of nformation than edges, and corners. Additionally, optimize on geometric reprojection error to achieve robust and easier optimization.
2. Average optical flow is similar to the overlap between two images.
