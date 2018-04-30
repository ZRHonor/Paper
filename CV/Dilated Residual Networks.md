Dilated Residual Networks
======================
Kaiming He

[paper](https://arxiv.org/pdf/1705.09914.pdf)

Work
-------------------------------
这篇文章实则是作者将何恺明(Kaiming He)博士残差网络Deep Residual Networks与其之前研究的Dilated Convolution相结合的结果。
* [Deep Residual Learning for Image Recognition ](https://arxiv.org/pdf/1512.03385.pdf)
* [Multi-Scale Context Aggregation by Dilated Convolutions ](https://arxiv.org/pdf/1511.07122.pdf)

Introduction
------------------------------
之前的卷积神经网络（Convolutional Networks）都是通过不断降低图像精度，直到图像被一个仅保留微弱空间信息的特征map表示（一般最后卷积层输出仅为7×7），最后通过计算类别概率来分类图像。这样情况下，尽管前面卷积网络做的很好，但是整个网络却不能获取一个十分精确的结果，例如一个很小的目标对解析图片信息十分重要，但是却被前面卷积网络因为过多降维和其体积很小而直接忽略掉了。

此外，图像分类的深度网络大多数还作为其他需要更多详细场景理解的任务的预训练模型，而很高的空间分辨率损失对这些任务而言是非常不利的。 

所以卷积神经网络应用在图像分类中，维护图片空间一定的分辨率是一个很重要的任务。现有算法有以下的做法： **up-convolutions**，**skip connections** 和 **other post-hoc measures**。但是上面的方法会造成图片变形，所以本文提出使用**Dilated Convolutions**方法来解决这个问题。Dilated Convolutions的好处就是既能保持原有网络的感受野（Receptive Field），同时又不会损失图像空间的分辨率（224×224输入的最后卷积层输出特征map是28×28）

上面实现过程总结来说就是，假设网络输入为28×28，我们使用padding和stride=1的卷积，卷积filter尺寸都是3×3。 
1.  输入28*28基础上3×3卷积，也就是经过1-dilated处理，感受野为 3×3，该操作和其他正常卷积操作一样，没有区别； 
2.  在(a)输出的基础上进行 3×3卷积，经过2-dilated处理，也就是隔一个像素进行与filter点乘最后相加作为中心像素的特征值，所以感受野变为 7×7； 
3.  在(b)的输出基础上进行 3×3卷积，经过4-dilated处理，也就是隔三个像素进行预filter点乘最后相加作为中心像素的特征值，所以感受野变为 15×15； 

由于filter卷积过程stride=1以及依靠padding，最后每层输出的特征map尺寸都依旧保持为28×28，和原图同样的大小。但是我们可以看到，网络无需借助池化层也能增大后续网络的感受野。

**Problem:**
最终输出maps会产生很差的网格状态（gridding artifacts）。作者主要通过Removing max pooling和Adding layers等操作一定程度上改善了最终输出结果。

Abstract
------------------------------
Convolutional networks for image classification progressively reduce resolution until the image is represented by tiny feature maps in which the spatial structure of the scene is no longer discernible. Such loss of spatial acuity can limit image classification accuracy and complicate the transfer of the model to downstream applications that require detailed scene understanding. These problems can be alleviated by dilation, which increases the resolution of output feature maps without reducing the receptive field of individual neurons. We show that dilated residual networks (DRNs) outperform their non-dilated counterparts in image classification without increasing the model's depth or complexity. We then study gridding artifacts introduced by dilation, develop an approach to removing these artifacts (`degridding'), and show that this further increases the performance of DRNs. In addition, we show that the accuracy advantage of DRNs is further magnified in downstream applications such as object localization and semantic segmentation. 