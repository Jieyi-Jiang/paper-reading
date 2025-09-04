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

Legged robots:

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

