# [Nature 2025] Controlling diverse robots by inferring Jacobian fields with deep networks

> Paper: [Controlling diverse robots by inferring Jacobian fields with deep networks](https://www.nature.com/articles/s41586-025-09170-0.pdf)

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

6. 之前的工作：有人利用过机器学习和基于标记的视觉伺服（marker-based visual servoing ）方法
   
   - 问题：应用到某个特定的机器人架构上时，需要大量的专家指导
