# DROID-SLAM: Deep Visual SLAM for Monocular, Stereo, and RGB-D Cameras (NeurIPS'21)

> Zachary Teed, Jia Deng

[Page Link](https://github.com/princeton-vl/DROID-SLAM)  

---
## System Overview
<img src="./assets/DROID-SLAM overview.png">

### Main structures
1. Differntiable REcurrent Optimization-Inspired Design(DROID), which is an end-to-end differentiable architecture that combines the strengths of both classical approaches and deep networks. Building upon RAFT for optical flow with introducing two key innovations.
- RAFT iteratively updates optical flow, DROID-SLAM iteratively update camera poses and depth updates on arbitrary number of frames, enabling joint global refinement.
- Each update is produced by a differentiable Dense Bundle Adjustment (DBA) layer, which computes Gauss-Newton update to dense per-pixel depth to maximize estimate of optical flow. Enables a monocular system to handle stereo or RGB-D input without retraining.

2. 
- 

---
### Improvements
1. 
