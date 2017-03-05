---
layout: post
title: TensorFlow Installation
categories:  [blog ]
tags: [Deep Learning ]
comments: true
published: true


---

TensorFlow Installation

我使用的方法是用virtualenv创建一个隔离的容器来安装TensorFlow，这样可以使得排查安装问题变得更容易。

在Mac上：

> sudo easy_install pip

> sudo pip install —upgrade virtualenv

接下来在 ~/tensorflow 目录下建立一个全新的virtualenv环境，执行：

> virtualenv --system-site-packages ~/tensorflow

> cd ~/tensorflow

然后激活virtualenv：

> source bin/activate  # 如果使用 bash

> (tensorflow)$  # 终端提示符应该发生变化

在 virtualenv 内, 安装 TensorFlow:

> (tensorflow)# pip install —upgrade<path of TensorFlow.whl>

> sudo pip install --upgrade https://storage.googleapis.com/tensorflow/mac/tensorflow-0.8.0-py2-none-any.whl

此时安装完成。

**运行TensorFlow**[Path:/Users/liujinglun/tensorflow]

```shell
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print sess.run(hello)
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print sess.run(a+b)
42
```