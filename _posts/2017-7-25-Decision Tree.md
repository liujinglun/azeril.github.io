layout: post
title: Decision Tree Note
categories:  [blog ]
tags: [Algorithm ]
comments: true
published: true

# Decision Tree学习笔记

**Decision Tree**

参考[机器学习算法与自然语言处理](https://zhuanlan.zhihu.com/qinlibo-ml)和机器学习(周志华版)

1. 在decision tree中，每个**非叶子节点**表示一个特征属性上的测试，每个分支表示这个特征属性在某个值域上的输出，每个叶子节点存放一个类别。
2. Decision Tree可以看做一个if-then规则的集合，我们需要从decision tree的根结点到每一个叶子结点构建一条规则。需要预测的实例都可以被一条路径或者一条规则覆盖。

Decision Tree：

- 由结点和有向边组成；
- 结点分内部结点和叶节点；
- 内部结点表示一个特征，叶节点表示一个类；

![Decision Tree](http://ww3.sinaimg.cn/large/006tKfTcly1fhvetww9tsj30xk0hywiq.jpg)

Decision tree表示实例属性值约束的合取得析取式。从树根到树叶的每一条路径对应一组属性测试的合取，树本身对应这些合取的析取。上图可以表示为

((纹理=清晰) ^ (根蒂=蜷缩)) V ((纹理=清晰) ^ (根蒂=稍蜷) ^ (色泽=乌黑)) V...((纹理=模糊))

决策树的判定过程相当于树中从根结点到某一个叶子结点的遍历。每一步如何遍历是由数据各个特征的具体特征属性决定。

**Decision Tree构建**

由上图可知，每一次子结点的产生，是由于在当前层数选择了不同的feature作为分裂因素。上图的特征包括纹理，根蒂， 触感，色泽。因此**Decision Tree的关键步骤是在某个结点处按照某一特征属性的不同划分构造不同的分支。**目标是让各个子集尽可能纯，即尽量让一个分类子集中待分类的项属于同一类别。判断纯的方法不同，对应不同的算法，包括ID3，C4.5和CART算法。

**ID3算法**

希望划分之后结点的“纯度”越来越高，则需要对纯度进行度量。**信息熵**是度量样本集合不确定性(纯度)的最常用的指标。在ID3算法中，采取information gain作为纯度的度量。即选取使得information gain最大的特征进行分裂。

**信息熵**代表随机变量的复杂度(不确定度)，**条件熵**代表某一个条件下随机变量的复杂度(不确定度)。

Information Gain = 信息熵 - 条件熵；

已知定义:当前样本集合D中第K类样本所占的比例为pk，则D的信息熵定义为

![information entropy](http://ww3.sinaimg.cn/large/006tKfTcly1fhvewh4mg4j30yw06iq3w.jpg)

离散属性a有V个可能的取值{a1, a2, …, aV}，属性a上取值为av的样本集合，记为Dv.

[例:离散属性为纹理，有3个不同的取值清晰，稍糊，模糊]

- 用属性a对样本集D进行划分获得的Information Gain为

![information gain](http://ww4.sinaimg.cn/large/006tKfTcly1fhvewdzvztj311q06sdmy.jpg)



- Information Gain表示得知属性a的信息而使得样本集合纯度减少的程度。
- 在Decision Tree中，如果选择一个特征后，information gain最大(信息纯度减少的程度最大)，那么我们就选择这个特征。
- ID3算法的缺点是information gain对可取值数目较多的属性有所偏好，会造成结果偏差[如：若把dataset中的编号作为候选划分属性，则其information gain很高，原因是每一个样本的编号都不同，由于编号唯一，条件熵为0，每一个结点中只有一类，所以纯度很高，这样导致只通过知道编号就可以进行判断，其他特征都没用了]。改进方法是使用Information Gain Rate来选择最优划分属性。



**C4.5算法**

![gain_rate](http://ww3.sinaimg.cn/large/006tKfTcly1fhvf1dbwbdj312o06ugo1.jpg)

![IV](http://ww1.sinaimg.cn/large/006tKfTcly1fhvf1q4393j30zy08440t.jpg)

- ID3算法对**可取数目较多的属性有所偏好**，因为当属性可取数目变多，分类变多，分到每一个子结点的纯度也就越大。这样造成部分属性在判断中所占比重过大，导致分类判断不准确。
- IV(a)可以反映出，当选取某种属性时，分成的V类别数目越大，IV(a)就越大，因此做分母可以减少属性分类过多的影响。
- C4.5算法的缺点是对**可取类别数目较少的特征有偏好**。改进措施是不直接选择information gain rate最大的候选划分属性，而在候选划分属性中找出information gain高于平均水平的属性，这样保证了大部分好的特征，在从中选择information gain rate最高的属性。

**Gradient Boost Decision Tree**

1.GBDT和RF都属于模型组合，将简单的模型组合使用，效果比单个更复杂的模型要好，组合的方法包括随机化(random forest)和boosting(GBDT).

2.Boosting方法

参考:http://www.cnblogs.com/LeftNotEasy/archive/2011/01/02/machine-learning-boosting-and-gradient-boosting.html

核心思想:建立M个比较简单的模型(如分类模型)，称为weak learner，每次分类将上一次分错的数据权重提高一点再进行分类。

训练集中一共有n个点，为训练集中的每个点赋上一个权重Wi(0<=i<n)，表示点的重要程度，通过依次训练模型的过程，对点的权重进行修正。在初始时期，所有点的权重相同，训练中**如果分类正确则权重降低，如果分类错了则权重提高**。程序越往后执行，则越会在意容易出错(权重高)的点。当全部程序执行完之后会得到M个模型，通过加权的方式组合成一个最终的模型。

3.Gradient Boosting

是一种Boosting方法，主要思想是每一次**建立模型是在之前建立模型损失函数的梯度下降方向**。损失函数描述模型的不靠谱程度，损失函数越大，则模型越容易出错。如果模型能让损失函数持续的下降，则说明我们的模型是在不停的改进，而最好的方法就是让损失函数在其梯度(Gradient)方向下降。

