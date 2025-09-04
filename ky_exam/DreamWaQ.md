# Dream WaQ: Learning Robust Quadrupeded Locomotion With Implicit Terrain Imagination via Deep Reinforcement Learning

## Basic Information 

1. Date: 2023, May, 29

2. Journal/Conference: ICRA 2023(2023 IEEE International Conference on Robotics and Automation), London, UK

3. Insititutions: Korea Advanced Institute of Science and Technology(KAIST，韩国科学技术院，韩国公立大学)

4. Home Page Link: [https://sites.google.com/view/dreamwaq](https://sites.google.com/view/dreamwaq)

5. Hardware: Unitree A1 (0k USD, 80k RMB)

6. Key Words: 

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

contributions of this work:

1. a novel locomotion learning framework 

    - asymmetric actor-critic architecture (非对称行动者-评论者架构)

2. a context-aided estimaotr network 

    - estimate body state and environmental context jointly

3. robustness and durability evaluation of the learned policy in the real world

    - the first demonstration of Unitree A1 walking on challenging terrain (hills and yards etc.)



## Dream WaQ

### A. Preliminaries (预备知识)

**Model - POMDP(Partially Observation Markov Decision Process, 部分可观测马尔可夫决策过程)**

full state:

$$
\mathcal{M}=(\mathcal{S}, \mathcal{O}, \mathcal{A}, d_{0}, p, r, \gamma)
$$


### B. Implicit Terrain Imagination 

teacher-student training paradigm 

- empirical, behavior cloning 

- data inefficient 

    - The student policy might be unable to explore failure states in which the teacher policy has learned in the early stage of learning using RL. 

asymmetric actor-critic architecture (非对称行动者-评论者架构)

proximal policy optimization (PPO, 近端策略优化) algorithm：

1. Policy Network 

    policy: $ ( \pi_{\phi} | \mathbf{a}_t, \mathbf{v}_t, \mathbf{z}_t ) $

    $ \mathbf{a}_t $ - action 

    $ \mathbf{o}_t $ - proprioceptive observation, measured directly from joint encoders and IMU

    $ \mathbf{v}_t $ - body velociy 

    $ \mathbf{z}_t $ - latent state, estimated by a context-aided estimator nework (CENet)

2. Value Network 

    Value Network's Role: Receiving the privileged observation, The value network is trained to output an estimation of the state value. （使用上帝视角，生成预测状态量，其输出用于作为训练时的参考数据，和policy的输出成对）

    privileged observation: 

    $
    \mathbf{s}_{t} = 
    \begin{bmatrix}
    \mathbf{o}_{t} & \mathbf{v}_{t} & \mathbf{d}_{t} & \mathbf{h}_{t}
    \end{bmatrix}^{T}
    $

    the policy network is trained to implicitly infer $\mathbf{d}_t$ and $\mathbf{h}_t$ from propriception. (diturbance force and height map)

3. Action Space 

    $12 \times 1 $ vector $\mathbf{a}_t$ - corresponding to the desired joint angle of the robot 

    $\mathbf{\theta}_{des} = \mathbf{\theta}_{stand} + \mathbf{a}_t$ : 基于站立时候的关节角度做偏置（这一个步骤是否真的必要，看起来有点类似于残差神经网络的假设）

4. Reward Function 

    closely follows other works to hightlight the effect of Dream WaQ's components instead of reward tuning

    task rewards - tracking the commanded velocity 

    stablity rewards - produce a stable and natural locomotion behavior 

    **印象深刻：居然可以使用强化学习去优化电机功率来减少发热以提高机器人运动距离。韩国人有点东西。**
    
5. Curriculum Learning
    
    terrains:

    - smooth

    - rough 

    - discretized 

    - stair terrains(with ten level inclination)

    grid-adaptive curriculum 


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

threefold - 三个方面的，三重性的，是学术论文中用于结构化表述贡献的标准术语。

to the best of our knowledge - 据我们所知

latent representation - 潜在表示，通过机器学习模型将高维原始数据（如传感器读数、地形图像）压缩为低维向量，其中每个维度编码数据的关键特征。
    
- 本文中：
    
    ​输入​：可能包含本体感觉历史数据、原始地形点云等

    ​输出​：低维连续向量 zₜ（通常32-256维）
    
    特性​：保留与运动控制相关的关键信息，过滤无关噪声

empirically - adv. 以经验为主的

data inefficient - 数据低效

interplay - n./v. 相互影响，相互作用

zero-shot sim-to-real - 零样本仿真-现实迁移；指在无需现实世界数据重新训练或微调的情况下，将仿真环境中训练的策略直接部署到物理机器人上并能正常工作。

inclination - 斜坡