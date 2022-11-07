# Robust reconstrution of indoor scene (ICCV'15)

> Choi. Sungjoon, Zhou. Qian-Yi, Koltun. Vladlen

[Page Link](http://redwood-data.org/indoor/index.html)  

---
## Review
### Main Structures
1. Fragment Construction
- Fragment(sequential 50 frames reconstructed point cloud) are reconstructed locally, and globally aligned fragment-wisely

2. Pose Algnment
- Graph optimization are conducted inter-fragment, intra-fragment based on correspondence information matrix.

---
### Improvements
1. Too many edge candidates(need to estimate relative pose, information matrix) to find, even if the local(fragment)-to-global hierarchical structure.
2. It depends highly on odometry sequential information, so it is hard to generally handle tracking failures.

