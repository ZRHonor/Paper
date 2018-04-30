# Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields

Zhe Cao

[paper](https://arxiv.org/pdf/1611.08050.pdf) [blog](https://blog.csdn.net/zhangjunhit/article/details/70308555) [gihub](https://github.com/ZheC/Realtime_Multi-Person_Pose_Estimation)

## Work

多人姿态实时估计



## Algorithm

输入一幅图像，经过卷积神经网络提取特征，得到一组特征图，然后分别使用CNN网络提取**Part Confidence Maps** 和 **Part Affinity Fields**，得到这两个信息后，使用图论中的**Bipartite Matching** 将同一个人的关节点连接起来得到最终的结果。

## Link

[Convolutional Pose Machines](https://github.com/ZRHonor/Paper/blob/master/CV/Convolutional%20Pose%20Machines.md)

