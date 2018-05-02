# Grid-based Motion Statistics for Fast, Ultra-robust Feature Correspondence

[paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8099785)

[项目主页](http://jwbian.net/gms)

[github](https://github.com/JiawangBian/GMS-Feature-Matcher)

## Work

将平滑度约束引入特征匹配是已知的可以实现超强鲁棒性匹配的方法。然而，这样的匹配方案既复杂又缓慢，使得它们不适合于视频应用。本文提出了GMS（基于网格的运动统计），一种简单的方法，将**运动平滑度作为一个统计量，进行局部区域的匹配**。GMS可以将高匹配数字转换成高匹配质量。 这提供了一个实时、超强的匹配系统。

论文GMS的方法实际上是消除错误匹配的一种方案，比如可以替换ransac。算法执行的大致流程是：**先执行任意一种特征点的检测和特征点的描述子计算，论文中采用的是ORB特征。然后执行暴力匹配BF，最后执行GMS以消除错误匹配。**

gms只是解决匹配的问题，ransac除了消除错误匹配，最重要的是得到了图像之间的投影变换矩阵。而且有一点，如果把特征点的数量弄到只有几百个，那最终的效果势必会大打折扣。

**在同样特征点个数的情况下，用ORB+BF+GMS  的时间 小于 SIFT + RANSAC的时间**

为了保证效果,特征点的个数就会很多。这时候ORB+BF+GMS的匹配效果要远好于SIFT+RANSAC,但整个时间可能和SIFT+SANSAC的时间相当甚至还要长。



## Abstract

Incorporating smoothness constraints into feature matching is known to enable ultra-robust matching. However, such formulations are both complex and slow, making them unsuitable for video applications. This paper proposes GMS (Grid-based Motion Statistics), a simple means of encapsulating motion smoothness as the statistical likelihood of a certain number of matches in a region. GMS enables translation of high match numbers into high match quality. This provides a real-time, ultra-robust correspondence system. Evaluation on videos, with low textures, blurs and wide-baselines show GMS consistently out-performs other real-time matchers and can achieve parity with more sophisticated, much slower techniques.