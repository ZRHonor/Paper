ECO : Efﬁcient Convolution Operators for Tracking
=============================================
Martin Danelljan

[paper](https://arxiv.org/pdf/1611.09224.pdf) [project](http://www.cvl.isy.liu.se/research/objrec/visualtracking/ecotrack/index.html) [github](https://github.com/martin-danelljan/ECO)


Result
-----------------------
极大的提升了Discriminative Correlation Filter(DCF)的速度，同时准确率性能有所提升。

Contributions
---------------------------------------------
* introduce a factorized convolution operator that dramatically reduces the number of parameters in the DCF model.
* a compact generative model of training sample space that effectively reduces the number of samples in the learing, while mainting their diversity.
* introduce an efficient model update strategy, that simulatneously improves tracking speed and robustness.

C-COT
------------------------------------------------
### advantage
* natural integration of multi-resolution feature maps
* the predicted detection scores of the target are directly obtained as a continuous function, enabling accurate sub-grid localization

ECO
-----------------------------------------
### Factorized Convolution Operator
First introduce a factorized convolution approach, with the aim of reducing the number of parameters in the model.

Instead of learing one separate filter for each feature channel d, we use a smaller set of basis filters. The filter for feature layer d is then constructed as a linear combination of the basis filters.

用很少的filter的线性组合来表示所有的filter

### Generative Sample Space Model
The standard sampling stratefy populates the whole training set with similar samples, despite containing almost the same information. Instead, we  propose to use a probabilistic generative model of the sample set that achieves a compact description of the samples by eliminating redundancy and enhancing variety.

视频中有大量连续的图像是相似的，提供的信息也几乎相同，因此可以将它们分组进行处理

### Model Update Strategy
Instead of updating the model in a continuous fashion every frame, we use a sparser updating scheme. Intuitively, an optimization process should only be started once sufﬁcient change in the objective has occurred. （只有充分多的改变发生后才进行优化）

We avoid explicity detecting changes in the objective and simply update the filter by starting optimization process in every Nth frame. （检测changes容易出现问题，直接设置每N次优化一次）

While increasing NS leads to reduced computations, it may also reduce the convergence speed of the optimization, resulting in a less discriminative model.

Abstract
----------------------------
In recent years, Discriminative Correlation Filter (DCF) based methods have significantly advanced the state-of-the-art in tracking. However, in the pursuit of ever increasing tracking performance, their characteristic speed and real-time capability have gradually faded. Further, the increasingly complex models, with massive number of trainable parameters, have introduced the risk of severe over-fitting. In this work, we tackle the key causes behind the problems of computational complexity and over-fitting, with the aim of simultaneously improving \emph{both} speed and performance. 

We revisit the core DCF formulation and introduce: (i) a factorized convolution operator, which drastically reduces the number of parameters in the model; (ii) a compact generative model of the training sample distribution, that significantly reduces memory and time complexity, while providing better diversity of samples; (iii) a conservative model update strategy with improved robustness and reduced complexity. We perform comprehensive experiments on four benchmarks: VOT2016, UAV123, OTB-2015, and TempleColor. When using expensive deep features, our tracker provides a 20-fold speedup and achieves a 13.0% relative gain in Expected Average Overlap compared to the top ranked method C-COT in the VOT2016 challenge. Moreover, our fast variant, using hand-crafted features, operates at 60 Hz on a single CPU, while obtaining 65.0% AUC on OTB-2015. 