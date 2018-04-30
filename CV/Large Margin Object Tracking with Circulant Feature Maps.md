Large Margin Object Tracking with Circulant Feature Maps
====================================================
Mengmeng Wang

[paper](https://arxiv.org/pdf/1703.05020.pdf) [知乎](https://zhuanlan.zhihu.com/p/25761718)

Conclusion
----------------------------------------------------------------------------
我们用了结构化SVM作为分类器，有着强大的判别能力，并引入了相关滤波，通过循环采样增加了训练样本的数量同时进行加速。我们利用多峰检测避免了相似物体和背景干扰。针对模型更新环节，提出了简单有效的模型更新策略，大大减少了模型漂移的情况，同时减少了模型更新的次数，达到了再次加速的效果。

Motivation
-----------------------------------------------------------------------------
### 算法思路
* 结合结构化SVM与传统SVM

`结构化SVM：这是一种输出空间可以是任意的复杂形式的SVM分类器，比如说序列、树等`

在基于相关滤波(Correlation Filter)算法出现之后，通过循环采样大大增加了样本数量，为一直以来困扰跟踪领域的稀疏采样问题提供了新的解决思路，并且可以用快速傅里叶变换FFT快速求解，因此可以在保证速度的前提下用一些维度较高的特征来做跟踪，比如KCF用到了HOG特征。KCF用简单的岭回归作为分类器，但是由于用到了高维的HOG特征以及稠密采样，使得它的效果还是非常好的，并且速度在170FPS左右，这也使得KCF变成了大量算法的baseline。

我们想`用循环矩阵来突破结构化SVM的稀疏采样问题，更想借助CF来突破结构化SVM的跟踪速度`。

### 针对前向跟踪
多峰前向检测。这一点是用来解决相似物体干扰的。在目标周围有特征相似的干扰物体时，响应图会有多个峰值，且最高的那一个有可能是干扰物体的，这时候可能就会引起误判。

### 针对模型更新
KCF的响应图（response map），在跟踪准确的时候是一个峰值很明显，接近理想的二维高斯分布图；而在跟踪的不好的情况中，尤其是遮挡、丢失、模糊等，响应图会剧烈振荡；因此我们提出了一种新的判据来判断是否出现了振荡，当判断出现振荡时，不进行模型的更新。这个判据的初始版本是我用在另一篇做机器人跟踪的文章中，[Real-time 3D Human Tracking for Mobile Robots with Multisensors (ICRA 2017)。](https://arxiv.org/abs/1703.04877)

LMCF Algorithm
-----------------------------------------------------------------------------
### 高置信度模型更新策略
如何判断跟踪结果是否准确是一个没有定论的问题，但又是一个非常重要的问题。因为这决定着模型的更新策略。KCF，DSST，DSSVM，Staple等许多算法是不进行跟踪结果可靠性的判定的，每一帧的结果都用来更新，或者像MDNet或者TCNN那样每隔N帧更新一次。这样是有风险的，特别是当目标被遮挡，或者跟踪器已经跟的不好的时候，再去更新模型，只会使得跟踪器越来越无法识别目标，这就是`模型漂移`问题，model drift。

由于想要保证跟踪速度，我们就需要一种简单有效的模型更新策略，最好能够通过已经获得的一些资源来进行判断，而不需要进行太多复杂的计算。首先最容易想到的就是response map的最高点的值Fmax，一般来说这个值越大说明跟踪的结果越好，但也有例外。

因此我们提出了一个新的判据`APCE`。这个判据可以反映响应图的振荡程度，当APCE突然减小时，就是目标被遮挡，或者目标丢失的情况，APCE相对于这段视频APCE的历史均值就减小的很明显，因此在这种情况下我们选择不更新模型，从而避免了模型的漂移。
只有当APCE和Fmax都以一定比例大于历史均值的时候，模型才进行更新，这样一来大大减少了模型漂移的情况，二来减少了模型更新的次数，达到了加速的效果。


Abstract
-------------------------------------------------------------------------------
Structured output support vector machine (SVM) based tracking algorithms have shown favorable performance recently. Nonetheless, the time-consuming candidate sampling and complex optimization limit their real-time applications. In this paper, we propose a novel large margin object tracking method which absorbs the strong discriminative ability from structured output SVM and speeds up by the correlation filter algorithm significantly. Secondly, a multimodal target detection technique is proposed to improve the target localization precision and prevent model drift introduced by similar objects or background noise. Thirdly, we exploit the feedback from high-confidence tracking results to avoid the model corruption problem. We implement two versions of the proposed tracker with the representations from both conventional hand-crafted and deep convolution neural networks (CNNs) based features to validate the strong compatibility of the algorithm. The experimental results demonstrate that the proposed tracker performs superiorly against several state-of-the-art algorithms on the challenging benchmark sequences while runs at speed in excess of 80 frames per second. The source code and experimental results will be made publicly available.