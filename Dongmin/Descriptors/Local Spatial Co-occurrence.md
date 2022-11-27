# An Efficient Online Loop Closure Detection System with Local Spatial Co-occurrence Information (IEEE Transactions of Industrial Electronics'22)

> Lijun Zhang, Weisheng Yan, and Huiping Li

[Paper Link](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9957088)  

---
## Review
### Problems of Related works
- The result of recognition on image can be easily affected by illumination, motion blur, viewpoint, or dynamic occlusion
- BoW-based schemes are robust to viewpoint, scale changes due to unordered quantization form. But, prone to lost the distinctiveness (quantization error occurs when voc is not rich enough to cover feature space).
- Hashing-based is hardly be established with no collision.
- VLAD(Vector of Locally Aggregated Desripotrs: One of BoW method) cna assemble quantization error with lossless tool in a relatively small vocaulary.
- Common KD-tree is fast but dificient in high dimensional space, a simple mean/medium merging is not reliable.

### Main Structures
<img src="./assets/Local Spatial Co-occurrence.png">
Efficient and novel BoW LCD system which can execute online. 
Paper aims to develop more informative and efficient feature representation with depth into the spatial relationship over images, where local co-occurrence information is exploited
- Local spatial co-occurrence relationship based on feature tracker, feature created into each BoW unit, voting-based decision scheme (temporal, similiarity)
- Hierarchical navigable small world graph-based vocabulary management module with online clustering, tailored for SURF descriptor
- Avoid preservation of historic images data

1. Place representation: the spatial information (mutual geometrical information between features) is exploited to retrain the local layout of each feature. As there exists loses while projecting 3D env into 2D image, system relies on the co-occurrence of adjacent features that counts the occurrence frequencies over the sequential images (counting the feature appearance of streamed input frames). Every features are tracked by KLT optical flow tracker. If the track length of feature over a threshold L_th, it assumed as a landmark. Tracking is refined with nearest neighbor in next frame. Pyramid size of each SURF feature is used to roughly offer the radius threshold.  
2. Incremental Database(Hierarchical Navigable Small World Graph): incrementally connecting to k-nearest neighbors for every inserted node. Continuously compute distance, which means automatic updates when find shorter route.
<img src="./assets/LCD alg.png" width=50%>

---
### Improvements
1. It needs to be sequential, Feature-wise word embeddings.
2. But get some intuition of graph structure.


### Notes
- Monocular SLAM chose to embed DBoW using handcrafted features SURF, ORB, matching based on Term Frequency-Inverse Document Frequency distance. But recall was bad. CNN features, Superpoint features, global feature and local attention based features. Sequence-Visual-Word-Vector was designed to use auxiliary information of sequential order, spatial transformation, feature co-ocurrence.
- No code is available
- Sequential input, tracking based, feature based descriptor

