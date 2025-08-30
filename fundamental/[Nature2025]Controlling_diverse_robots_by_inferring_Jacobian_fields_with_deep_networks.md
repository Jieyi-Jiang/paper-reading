# [Nature 2025] Controlling diverse robots by inferring Jacobian fields with deep networks

> Paper: [Controlling diverse robots by inferring Jacobian fields with deep networks](https://www.nature.com/articles/s41586-025-09170-0.pdf)

## 总结

1. 用到的关键技术点和基础理论
   
   1. Neural Radiance Fields 神经辐射场 (3D reconstruction)  -> NeRF
   
   2. Self-supervised learning method 
   
   3. optical flow and point-tracking methods
      
      跟踪机器人的运动，作为训练的参考数据（真实数据）
   
   4. **volume** rendering 体渲染  (3D reconstruction) -> NeRF
      
      让单目相机具有3D感知的能力
   
   5. Differentiable rendering 可微分渲染

2. 这个方法诞生的必要条件
   
   1. 机器学习
   2. 算力（半导体，计算机）
   3. 图像处理

3. 之前为什么没有人想到这个方法

4. 启发
   
   - 无监督学习和有监督学习
     
     想要进行大规模、长时间的持续训练，肯定是要用到无监督的方法的，纯有监督的方法已经过时了。有监督学习可以作为一种调优的手段。
   
   - 无监督学习和强化学习
     
     这两个结合有希望碰撞出火花，但是应该怎么结合呢？  
   
   - 从本质上来说，这是一个机器人 **自学习** 的过程
     
     1. 关节指令随机采样 - 尝试控制机器人的躯体
     
     2. 使用相机拍摄关节的运动，观察/感受躯体的运动
     
     3. 无监督训练。控制身体，观察身体运动，并从中学习出怎么样控制身体去完成期望的运动动作。
     
     4. 类似于婴儿学习走路，不断试错，不断观察，不断学习。非常棒的思路，非常的仿生。

## Introduction

### 1 需求

- 可能性：现代制造技术有望带来新一代收大自然启发的机器人系统。

- 传统机器人：由独立关节连接的刚体连杆。

- 仿生机器人：结合软体、柔性材料和刚体部分，组成“柔-刚混合”系统。
  
  - 更适应于多变的环境
  
  - 和人类协作时更安全

- 柔刚混合机器人的问题（本文着重解决的问题）
  
  1. 难以建模（However, the use of bio-inspired hardware is hindered by our limited capability to model these systems）
  
  2. 传统的控制方法，需要机器人本体和机器人模型相互“孪生”，才能精确预测机器人关键部分（比如末端执行器）在所有时间所有指令下的运动。

### 2 传统机器人（机械臂）

传统机器人的设计是为了更加方便建模和控制（而不是更容易和世界进行“交互”）

- 使用高精度加工的部件，precision-machined parts

- 使用高刚性的材料来制造零件，high-stiffness materials（杨氏模量从 $10^9 - 10^12 Pa$）

- 机械臂由低公差的关节连接（low-tolerance joints）

- 充分建模为理想刚体连杆组成的运动学链

- 还需要在每一个关节使用高精度传感器，从而实现机械臂的可靠3D重建

- 在这里，专家可以可靠地在所有可能的运动指令下建模机器人运动并设计控制算法去执行期望的运动。（With this in place, an expert can reliably model the motion of the robot under all possible motor commands and design control algorithms to execute desired motions.）

### 3 软体和仿生机器人

1. 最大的问题：难以建模

2. 制造材料：与软体生物材料（组织、肌肉和肌腱）的刚度相匹配

3. 这些材料的特点：在动作的时候，遭受大的形变，并展现出“时间依赖特性”（例如“粘弹性”，和反复的加负载和去负载时，展现出逐渐的弱化特性）

4. 数学描述：产生自“连续介质力学与大变形理论（continuum mechanics and large deformation theory）” 的微分方程描述了软体材料的行为，但是要求解这些微分方程，成本高昂（算力成本），特别是对于控制和实时应用中。

5. 方程化简：模型降阶法（Model order reduction methods），几何近似法（Geometrical approximation methods），刚性离散化方法（Rigid discretization methods）
   
   - 问题：高度依赖于特定系统的简化假设，不能普遍的推广使用

6. 之前的工作：
   
   1. 有人利用过机器学习和基于标记的视觉伺服（marker-based visual servoing ）方法
      
      - 问题1：应用到某个特定的机器人架构上时，需要大量的专家指导。
      
      - 问题2：高精度运动捕捉系统（High-Precision Motion-Capture System），昂贵、笨重需要可控的使用环境。
   
   2. 机器人形态学的神经网络场景表达
      
      - 问题1：依赖于一些高精度的嵌入式传感器，但是难以在仿生和软体机器人中安装此类传感器。
      
      - 问题2：依赖于3D动作捕捉实现高精度控制。

7. 总结：我们需要的是一种通用的控制方法，这种方法不依赖于机器人系统装配工艺、执行器（驱动方式）、嵌入式传感器、材料和形态。

### 4 本文提出的新方法（Visuomotor Jacobian Field）

## Visuomotor Jacobian Field - 视觉-运动雅可比场

#### 我的思考

1. 如果从传统的机器人的角度来看的话。传统的机器人是在关节空间 $\\bm{q}$ 下进行规划，而本文则是越过关节空间，通过神经网络和纯视觉的方法直接在笛卡尔空间 $\bm{x}$ 下进行规划。如果这里的 **2D图片空间** 和 **3D空间** 可以视作 **笛卡尔空间**的话

2. 还是不够泛化，只能根据不同的机器人训练不同的  Visuomotor Jacobian Field 。模型本质上并不具备**理解物理世界**的能力，如果需要更加泛化的**机器**，需要训练出一个能真正理解物理世界的模型。

两个重要组成部分：

1. 状态预测模型（state-estimation model）：从单视频流中，推理出机器人的3D表示，通过对机器人的3D几何和微分运动学进行编码（每个3D的点在任意可能的指令下，将如何运动）。

2. 逆动力学控制（inverse dynamics controller）：在2D图片空间或3D空间以**交互速度**对期望的机器人运动进行**密集参数化**。

主要的公式：

## 相关名词

inverse dynamics controller - 逆动力学控制

neural radiance field - 神经网络辐射场

differential kinematics - 微分运动学

case-by-case basis - “一事一议”原则

visuomotor Jacobian Field - 视觉-运动雅可比场，体现了视觉的点和机器人关节运动之间的雅可比（微分）关系的场

linearity and spatial locality inductive biases - 线性归纳偏置和时间局部归纳偏置

unseen robot configuration - 未见机器人构型，configuration在这里不是配置的意思，而是构型的意思，指的是机器人的形态。未见机器人构型应该是训练中没有见到的样例，对 unseen robot configuration 的预测精度体现了模型的泛化能力。

volume rendering 体渲染

differentiable rendering 可微分渲染
