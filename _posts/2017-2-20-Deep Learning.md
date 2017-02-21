---
layout: post
title: Python
categories:  [blog ]
tags: [Deep Learning]
comments: true
published: true


---

# Python Deep Learning

1.深度学习是机器学习的一个分支，它基于试图使用包含复杂结构或由多重非线性变换构成的多个处理层对数据进行高层抽象的一系列算法。

2.导数是单变量的变化率，偏导数是**当有多个变量时针对某个变量的变化率**。

3.深度学习是采用神经网络，用于解决线性不可分的问题。深度学习即具有多个hidden layers的神经网络。深度学习是一个不断磨合的过程，刚开始定义一个标准参数，之后不断进行修正，得出每个节点间的权重。

4.概念：

- 激活函数

  ![2](https://ww4.sinaimg.cn/large/006tNc79gy1fcxqhy6varj30x20oktcs.jpg)

- 学习系数[Weights and Biases]

- 损失函数(Lost Function)

  - Loss is the distance between the network output and target.

  - Loss of all examples should be as small as possible.

    ​

5.Train and Test:

![1](https://ww4.sinaimg.cn/large/006tNc79gy1fcxqff5980j30x60ou13y.jpg)

6.Three Steps for Deep Learning

(1)Define a set of function:

- **Neural Network**
- Given network structure, define a function set.

(2)Goodness of function;

- 使损失函数(function loss)最小化；
  - Find a function in function set.
  - Find the network parameters 𝜃;
  - Network parameters 𝜃 = [𝑤,𝑤,⋯,𝑏,𝑏,⋯]

(3)Pick the best function.

- Find network parameters 𝜃 that minimize total loss L;
- Gradient Descent;计算偏导数Compute 𝜕𝐿/𝜕𝑤;

![1](https://ww2.sinaimg.cn/large/006tNc79gy1fcxsvuio9vj30xm0oojxq.jpg)

![](https://ww1.sinaimg.cn/large/006tNc79gy1fcxsw37p1sj30xs0po0xx.jpg)

![](https://ww2.sinaimg.cn/large/006tNc79gy1fcxsw4war7j30xi0oqgr4.jpg)

Difficulty:Gradient descent never guarantee global minima

- 梯度下降不保证全局最小值。
- 使用不同的initial point会到达不同的minima，导致不同的结果。
- 解决方法：Backpropagation 回溯[反向传播]
  - 可以有效解决𝜕𝐿/𝜕𝑤问题；

7.深入Deep Learning:

使用Thin+Tall的神经网络(多层结构，每层节点数量较少)而不是Fat+Short(单层结构，每层节点数量多)的原因是Thin+Tall通常包含更多train data。所以精度更高。

8.深度学习框架:

- Keras:
  - Interface of TensorFlow or Theano;
  - Flexible, easy to learn and easy to use.









