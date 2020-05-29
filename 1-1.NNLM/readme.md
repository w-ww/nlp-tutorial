NNLM
https://towardsdatascience.com/deep-transfer-learning-for-natural-language-processing-text-classification-with-universal-1a2c69e5baa9



http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf
怎么这么难懂...
https://medium.com/@satyavasanth_57235/yoshua-bengios-a-neural-probabilistic-language-model-in-500-words-665b6e64ade6

怎样理解 Curse of Dimensionality（维数灾难）
https://zh.wikipedia.org/wiki/%E7%BB%B4%E6%95%B0%E7%81%BE%E9%9A%BE
https://www.zhihu.com/question/27836140

distributed representation (分散式表示)向量的每一维都表示文本的某种潜在的语法或语义特征
https://zhuanlan.zhihu.com/p/22386230
一、文本表示
首先，我们先来看下什么是文本表示。文本表示，也可以称为语言表示，是对人类语言的一种描述或约定，是认知科学和人工智能等多个领域共同存在的问题。在认知科学里，语言表示是语言在人脑中的表现形式，关系到人类如何理解和产生语言（注：配图就出自于今年很轰动的那篇大脑词汇图的论文）。在人工智能里，语言表示是主要指用于语言的形式化或数学的描述，以便在计算机中表示语言，并能让计算机程序自动处理。我们常说的词向量就是向量的形式来表示一个词。
语言具有一定的层次结构，并且可以划分为不同的语言粒度（比如，词、短语、句子、段落以及篇章）。这些不同的粒度文本都有相对应的表示。

二、文本分布式表示
说到文本的分布式表示，有一定NLP背景的人都会想到两个不同英文术语。一个是Distributional Representation，另一个是Distributed Representation。这两个术语都翻译为分布式表示，因此很多人混淆。但是，这两个术语的含义和出发点完全不一样。

Distributional Representation是从分布式假设（即如果两个词的上下文相似，那么这两个词也是相似的）的角度，利用共生矩阵来获取词的语义表示，可以看成是一类获取词表示的方法。这里的“分布”带有统计上分布的意思。我们可以构建一个大小为W×C的共现矩阵F，其中W是词典大小，C是上下文数量。上下文的类型可以为相邻词、所在句子或所在的文档等。共现矩阵的每一行可以看作对应词的向量表示。基于共现矩阵，有很多方法来得到连续的词表示，比如潜在语义分析模型（Latent Semantic Analysis, LSA）、潜在狄利克雷分配模型（Latent Dirichlet Allocation，LDA）、随机索引（random indexing）等。

而Distributed Representation中的distributed 没有统计上的“分布”含义，而是“分散”、“分配”的意思。一段文本的语义分散在一个低维空间的不同维度上，相当于将不同的文本分散到空间中不用的区域。Distributed Representation是文本的一种表示形式，具体为稠密、低维、连续的向量。向量的每一维都表示文本的某种潜在的语法或语义特征。Distributed Representation翻译为分散式表示可能理解起来会更明确些。


我经常会以下面这幅围棋棋盘来说明是什么是Distributed Representation。以词为例，如果我们有100个词，相当于100个棋子。如果用onehot方式来表示，我们需要建立100维的空间。但是现在，我们只需要建立一个二维的空间，在里划分很多格子（格子数量大于100个），然后把这些棋子（词）分散地放在不同的格子上。格子的坐标代表了相应的棋子（词）的向量表示。这样就相当于在两维的空间中表示了100个棋子（词）。

[![Foo](https://pic1.zhimg.com/80/d6a33408a8bf47e3af5b3f9623233fd4_720w.jpg)](https://zhuanlan.zhihu.com/p/22386230)


这里需要强调一点的是，这种“分散式表示”只要在低维的空间中能够区分出两个词的不同就够了。不一定非得要求意义相近的词距离也相近。因为上层的神经网络可以具有高度非线性，完全可以将原始的表示空间高度扭曲。所以，从Distributed Representation本身来讲，我们不要给它附加太多的意义，比如要满足man−woman ≈ king – queen之类的。Distributed Representation就是将文本分散在低维空间中的很多点上，只要这些点有一定区分性就够了。说得极端一点，我们的词向量都是随机产生的稠密向量，这也是一种distributed表示，不需要有语义上解释（比如分布式假设）。只要后续的模型足够强大，一样可以做的很好。


总之，Distributional Representation指的是一类获取文本表示的方法，而Distributed Representation指的是文本表示的形式，就是低维、稠密的连续向量。

但这两个并不对立。比如Skip-Gram、CBOW和glove等模型得到词向量，即是Distributional Representation，又是Distributed Representation。
