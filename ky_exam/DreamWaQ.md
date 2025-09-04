# Dream WaQ: Learning Robust Quadrupeded Locomotion With Implicit Terrain Imagination via Deep Reinforcement Learning

## Basic Information 

1. Date: 2023, May, 29

2. Journal/Conference: ICRA 2023(2023 IEEE International Conference on Robotics and Automation), London, UK

3. Insititutions: Korea Advanced Institute of Science and Technology(KAIST，韩国科学技术院，韩国公立大学)

4. Code: [GitHub(may be?)](https://github.com/Manaro-Alpha/DreamWaQ)

5. Key Words: 

    - Deep Reinforcement Learning

    - Quadrupedal robots 

    - Unstructured Terrain

## Introduction 

Legged robots：

1. good: can traverse unstructured terrains 

2. bad: difficulty to control

文章改进的点：

1. model-based 的方法太废柴

    - complex pipline: 

        - state estimation

        - trajectory optimization 

        - gait optimization (步法优化) 

        - actuator control 

    - requires considerable human effort 

        - accurate modeling 

        - rigorous parameter tuning 

    - linearization of quadrupedal model limits its performance

2. legged animals 很牛逼，要学习（Legged animals can effificiently plan their gait by visually perceiving the surrounding terrains.）


对比外部传感器和内部/本体传感器（exteroceptive sensors and proprioceptive sensors）

dilemma:

1. The policy needs to understand the terrain properties to learn robust behavior. 

2. To adequately learn the terrain properties, the robot should be able to walk accordingly and explore a wide spectrum of terrain properties.


## Dream WaQ

### A. Preliminaries 

### B. Implicit Terrain Imagination 

### C. Context-Aided Estimator Network 

## Experiments 

### A. Compared Methods 

### B. Simulation

### C. Real-Word Experimental Setup

### D. Command Tracking 

### E. Explicit Estimation Comparison 

### F. Robustness Analysis 

### G. Long-Distance Walk 

## Conclusion 



## Words 

malfunction - v. 失灵，出现故障 to fail to work correctly 

pliable - adj. 易弯曲的；柔韧的 easy to bend without breaking 

modality - 形式，样式，形态 the particular way in which sth exists, is experienced or is done

empirical - adj. 经验主义的，以实验/经验为依据的  based on experiments or experience rather than ideas or theories 

bottleneck - n. 瓶颈






