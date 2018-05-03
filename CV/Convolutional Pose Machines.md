# Convolutional Pose Machines

Shih-En Wei

[paper](https://arxiv.org/pdf/1602.00134.pdf) [blog](https://blog.csdn.net/shenxiaolu1984/article/details/51094959) [github](https://github.com/shihenw/convolutional-pose-machines-release)



## Work

1. 用**各部件响应图来表达各部件之间的空间约束**。响应图和特征图一起作为数据在网络中传递。
2. 网络分为多个阶段（stage）。**各个阶段都有监督训练**，避免过深网络难以优化。
3. 使用同一个网络，同时在多个尺度处理输入的特征和响应。既能确保精度，又考虑了哥哥不见之间的远距离关系。

## Algorithm

1. 在每个尺度下，计算各个部件的响应图
2. 对于每个部件，累加所有尺度的响应图，得到总响应图
3. 在每个部件的总响应图上，找出响应最大的点，为该部件位置

## Net Structure

参见[paper](https://arxiv.org/pdf/1602.00134.pdf)和[blog](https://blog.csdn.net/shenxiaolu1984/article/details/51094959)



## Abstract

Pose Machines provide a sequential prediction framework for learning rich
implicit spatial models. In this work we show a systematic design for how
convolutional networks can be incorporated into the pose machine framework for
learning image features and image-dependent spatial models for the task of pose
estimation. The contribution of this paper is to implicitly model long-range
dependencies between variables in structured prediction tasks such as
articulated pose estimation. We achieve this by designing a sequential
architecture composed of convolutional networks that directly operate on belief
maps from previous stages, producing increasingly refined estimates for part
locations, without the need for explicit graphical model-style inference. Our
approach addresses the characteristic difficulty of vanishing gradients during
training by providing a natural learning objective function that enforces
intermediate supervision, thereby replenishing back-propagated gradients and
conditioning the learning procedure. We demonstrate state-of-the-art
performance and outperform competing methods on standard benchmarks including
the MPII, LSP, and FLIC datasets.
