# Habitat2.0: Training Home Assistants to Rearrange their Habitat (NeurIPS '21)

> Andrew Szot, Alex Clegg, Eric Undersander, Erik Wijmans, Yili Zhao, John Turner, Noah Maestre, Mustafa Mukadam, Devendra Chaplot, 
Oleksandr Maksymets, Aaron Gokaslan, Vladimir Vondrus, Sameer Dharur, Franziska Meier, Wojciech Galuba, Angel Chang, Zsolt Kira,
Vladlen Koltun, Jitendra Malik, Manolis Savva, Dhruv Batra

[Page Link](https://github.com/facebookresearch/habitat-sim)  

---
## Review
*** This review is Not fully covered. Just manual parts for understanding how the simulator works

### Main Structures
<img src="./assets/Habitat2.0 ReplicaCAD.png">
1. Dataset: ReplicaCAD, synthethic apartment space from Replica dataset including dynamic objects and interactive available object.   
2. Simulator: physics-enabled 3D simulator. Using 8-GPU makes 850 x real-time reinforcement training.   
- What is simulator? two components, H2.0 uses a deep low-level integreation(C++).   
  (1) A physical engine that evolves the world state s over time s_t->s_t+1 (via Magnum).  
  (2) A renderer that generates sensor observations o from states: s_t->o_t (via Bullet).   

### Improvements



### Notes


