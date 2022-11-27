# An Efficient Online Loop Closure Detection System with Local Spatial Co-occurrence Information (IEEE Transactions of Industrial Electronics'22)

> Lijun Zhang, Weisheng Yan, and Huiping Li

[Paper Link]([https://www.sciencedirect.com/science/article/pii/S0169023X05000819](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9957088))  

---
## Review
### Problems of Related works
- The result of recognition on image can be easily affected by illumination, motion blur, viewpoint, or dynamic occlusion
- BoW-based schemes are robust to viewpoint, scale changes due to unordered quantization form. But, prone to lost the distinctiveness (quantization error occurs when voc is not rich enough to cover feature space).
- Hashing-based is hardly be established with no collision.
- VLAD(Vector of Locally Aggregated Desripotrs: One of BoW method) cna assemble quantization error with lossless tool in a relatively small vocaulary.
- Common KD-tree is fast but dificient in high dimensional space, a simple mean/medium merging is not reliable.

### Main Structures
<img src="./assets/Local%20Spatial%20Co-occurence.png">
Efficient and novel BoW LCD system which can execute online. 
Paper aims to develop more informative and efficient feature representation with depth into the spatial relationship over images, where local co-occurrence information is exploited
1. Local spatial co-occurrence relationship based on feature tracker, feature created into each BoW unit, voting-based decision scheme (temporal, similiarity)
2. Hierarchical navigable small world graph-based vocabulary management module with online clustering, tailored for SURF descriptor
3. Avoid preservation of historic images data

---
### Improvements


### Notes
- Monocular SLAM chose to embed DBoW using handcrafted features SURF, ORB, matching based on Term Frequency-Inverse Document Frequency distance. But recall was bad. CNN features, Superpoint features, global feature and local attention based features. Sequence-Visual-Word-Vector was designed to use auxiliary information of sequential order, spatial transformation, feature co-ocurrence.

