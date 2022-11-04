# BundleFusion: Real-time globally consistent 3d reconstruction using on-the-fly surface reintegration (ToG'17.05)

> Angela. Dai, Niessner. Matthias, Zollhofer. Michael, Iadi. Sharam, Theobalt. Christian

[Page Link](https://graphics.stanford.edu/projects/bundlefusion/)  

---
## System Overview
<img src="./assets/BundleFusion overview.png">

### Main structures
1. On GPU, SIFT features are detected, matched with previous features, filtered based on geometric and photometric consistency.
- Estimate rigid transformation Tij minimizing RMSD by Kabsch alg
- Condition analysis of covariance, cross-covariance and filter (>100)
- Correspondence filtering by reprojection error (residual>0.02m)
- Surface filtering: spanning by correspondence should bigger than 0.032m^2
- Downsampled input dense verification: reprojection discrepancy (<0.15m), normal deviation (>0.9), photoconsistency (0.1)
- Cache remaining correspondences (Frame-to-frame Use 5 correspondences)

2. Hierarchical Optimization
- Chunk(sequential 11 frame) are pose optimization with valid feature correspondences and dense photometric and geometric matching
- If reprojection error is too large for any inter-chunk frame pair (>0.05m), chunk discarded
- Keyframe is first frame of chunk.
- Global loop closure is finding using keyframe's feautures, aggregate with previously found keyframe features (merged <0.03m)
- If keyframe feature doesn't have good features, remain it as candidate
- Every frame-wise matches are optimized using energy minimization considering both sparse and dense alignment 

3. Energy Minimization
- Weights of dense energy is linearly increased allowing coarse to fine alignment
- Sparse energy is calculated in correspondence features
- Dense energy is calcuated in both photometric and geometric.
- 

---
### Improvements
1. Too many heuristic filters (From correspondence finding, Chunk finding, loop finding

