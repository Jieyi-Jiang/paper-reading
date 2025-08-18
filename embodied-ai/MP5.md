# MP5: A Multi-modal Open-ended Embodied Systemin Minecraft via Active Perception

---- 

link of paper: [[2312.07472] MP5: A Multi-modal Open-ended Embodied System in Minecraft via Active Perception](https://arxiv.org/abs/2312.07472)

bilibili: [【CVPR'24】MP5：当多模态大语言模型遇上具身智能](https://www.bilibili.com/video/BV1ieHmerEJF)

youtube: [MP5: A Multi-modal Open-ended Embodied System in Minecraft via Active Perception - YouTube](https://www.youtube.com/watch?v=AZeS3C_S_3M)

---

# 解决了什么问题

## 想要解决什么问题

> One of the core objectives of current embodied intelligenceis to construct generalist agents that can solve long-horizonopen-world embodied tasks, approaching the behavior pat-terns of human beings [1, 19, 22, 31].

『构建一个可以解决长时域开放世界具身任务的通用智能体，接近人的行为模式。』

PS：现在的科研思路还是**构建**一种智能体去模仿人的行为模式，能不能有一种方法，直接生成一种类似于生物的智能体，只需要规定一些基本规则，自由的生成框架和参数。

## 存在的问题（困难）

- 任务本身的困难：
  
  1. Process Dependency，流程依赖。任务子流程之间存在内在依赖。不只是简单的顺序问题，在更复杂的问题里面，各个子流程，可能是相互依赖的。如果只是一个顺序问题，那么子任务可以构成一个序列；如果是更复杂的依赖，则子任务会形成一个图。
  
  2. Context dependency，语境依赖。子任务的执行依赖于环境信息。任务和环境之间，存在交互关系。

### 解决思路



# 新的想法

1 智能体集群

# Framework

系统框架：

- 1 Planner

- 2 Parser

`1`  and `2`  is **Zero-Shot Large Language Model** : GPT4 or Llama

- 3 Precipient - trainning by themselves 
  
  - Mutlimodal large model(多模态大模型): Nvidia MineDOJO - Mineclip
  
  - Align the vision encoder to Llama
  
  - Be similiar to the trainning method of the Llava
  
  - It doesn't train the Alignment Net beforehand, but trains the multimodal large model (whole model) end to end. 

训练数据：

- 调用MINEMDOJO 里面的 RL 的 Polic，然后获得多场景、多生物，基本覆盖 Minecraft 里面所有场景的数据集。 (Instruction tuning dataset )

# Drawback

1. 依然不能算作为真正的智能，也不能算做真正的思考。只是利用大模型的文本能力去“局部”规划，并不利用 MineCraft 的游戏规则去完成一个大的任务或者自由探索。

2. 怎么去定义我所说的问题，怎么定义`智能`和`思考` ，怎么证明我说的问题是存在的？

# Vocabulary

generalist agents - 通用型智能体

long-horizon open-world embodied tasks - 长时域开放世界具身任务

process dependency - 流程/过程依赖

context dependency - 语境/上下文依赖

aforementioned goal - 上述目标

inherent dependency - 固有的依赖关系
