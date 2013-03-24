---
layout: default
published: false
---

# How does it work?

Enter Text in Markdown format.

Graphical Model（概率图模型）的浅见
ASIDE ·	 13. 一月 2013 · Write a comment	 · Categories: 互联网
最近在做一些概率图模型的东西，所以有一点点浅见，就随便写写，白话、不带数学公式，不深。
概率图分为有向图（bayesian network）与无向图（markov random filed）。直觉上说，有向图突出causality（因果关系，其实只是correlation），无向图突出correlation（关联性）。为什么用图模型，我觉得主要原因还是为了更好的捕获随机变量间的关系。像SVM、Decision Tree、Regression等模型通常假设分类结果只依赖于既有的特征，并没有直接捕获（观察到的与观察不到的）随机变量之间的复杂关系，虽然在特征充足的情况下效果还是不错，但这在某些问题中会变得非常局限（比如判断A的分类不仅跟A的特征有关，跟B的分类也有关的时候）。在概率图上可以建立生成模型或判别模型。有向图多为生成模型（如LDA、HMM），无向图多为判别模型（如CRF）。过去的报告认为判别模型在分类问题上比生成表现更加好（比如Logistic Regression与Naive Bayesian的比较，再比如HMM与Linear Chain CRF的比较）。当然，生成模型的图模型也有一些难以代替的地方，比如更容易结合无标注数据做semi-or-un-supervised learning。
用概率图模型去解决问题，第一步是把模型建立起来，有哪些随机变量，他们之间是什么关系，如何互相作用，用有向图还是无向图，生成模型还是判别模型，等等。这个过程是第一步，但又不只是第一步，有些数据间的关系不是那么直觉的，用拍脑袋想出来的模型往往是需要验证与修改的。因为叫做概率图模型，所以几乎肯定是带参数，所以设计好模型后，要做的就是parameter estimation。这些参数一般要学出来，有很多种学的方法，比较常用的是ML(maximum likelihood)，也就是先写一个似然函数，然后最大化似然函数来求参数，最大化的方式可以是梯度下降、牛顿法、各种拟牛顿法、SGD（随机梯度下降）等。得到参数后，就可以用model去做classification啊、prediction啊什么的，通通需要inference，就是求posterior marginal probability，最大化总体的posterior marginal probability。inference的方法也有很多种，比较常用的，用来求marginal probability的：Sum Product（也叫Belief Passing、Message Passing）、MCMC、Varational等，用来求最大化marginal probability的：Max Sum等等。因为有向图与无向图其实都可以化作一种统一的形式：Factor Graph（因子图），并且在这种图上做parameter estimation和inference都比较方便(上面说的BP等也是针对这种图的)，所以很多时候，模型都直接用FG来表示。
概率图模型”博大精深”，由于其对随机变量间关系的出色的model能力，不错的learning与inference效果，以及日渐增多的问题都会遇到图状随机变量集，它应该会有越来越应用广泛。概率图模型比起SVM等可能还是要相对处于年幼期，虽然已经被用了很久，但是还有很多问题可以改进（比如在inference中approximation的收敛性和准确度）。想起上次龙星计划，好多人问概率图模型最近这么热但比起传统的模型究竟有多大前进？我觉得还是在处理不太一样的问题吧，直接的比较并不是特别合适（如果要比，一般要忽略变量间关系，然后用SVM等方法去做，效果往往会更差；相反，在一些非常特殊的问题上，如果有办法把这种关系融合到一些特征中去，使得随机变量能够相对独立，用BP等方法的GM也可能由于approximation而比不过SVM）。但是，在SVM专攻的方向上，也有图模型或者说网模型介入挑战了，那就是deep learning，deep learning跟graphical model有很多相似之处，虽然解决的问题与具体方法不太一样，但是网状结构的模型还是很类似的。这是不是在说明，explicitly去model（observable and unobservable）变量之间的关系与结构或许是未来的一个重要方向呢？

