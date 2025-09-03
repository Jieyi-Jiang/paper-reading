# BeyondMimic: From Motion Tracking to Versatile Humanoid Control via Guided Diffusion

## Basic Information 

1. Date: 2025.8.11

2. Institutions: University of California, Berkeley(UCB), Stanford
 University

3. Journal/Conference: preprint on Arxiv

4. Home Page Link: [https://beyondmimic.github.io/](https://beyondmimic.github.io/)

5. Goal: Reproducing a given reference motion on robot hardware with high quality in global coordinates.

## Chanllenges

1. Gap Between Simulation and Real-World

2. Deployment difficulty:

    1) a scalable, high-quality motion tracking framework

    2) an effective sim-to-real recipe to distill learned motion primitives into a single policy

## Solution and Technology

### Framework

1. Motion tracking pipline 

2. Guided diffusion policy

### Technical Points 

1. Reinforcement Learning 

2. Motion Tracking (Scalable Motion Tracking)

    1) unified MDP(Markov Decision Process)

        - MDP - 强化学习中的经典数学模型，用于描述智能体（如机器人）在环境中的决策过程

            MDP 四要素：
        
            (1) 状态 State
        
            (2) 动作 Action 
            
            (3) 状态转移概率 State Transition Probability
            
            (4) 奖励函数 Reward Function 
           

        - Unified MDP - 将所有运动跟踪任务抽象为同一套MDP公式

    2) a single set of hyperparameters

3. Diffusion-based Controller (First Guided Diffusion for Humanoids)

4. End-to-End 

### Dataset



## Words

overfit - 过拟合

domain randomization - 邻域随机化

kinematic diffusion model - 运动学扩散模型
N
out-of-distribution 

infrequent - 低频的，罕见的，不频发的

frequent - 高频的，频繁的

torso - 躯干




