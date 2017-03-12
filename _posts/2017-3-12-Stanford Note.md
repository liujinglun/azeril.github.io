---
layout: post
title: Note for TensorFlow Course by Stanford
categories:  [blog ]
tags: [Deep Learning]
comments: true
published: true


---

#### Note

- Tensor = An n-dimensional matrix.
  - 0-d: scalar(number)
  - 1-d: vector
  - 2-d: matrix

![w](https://ww4.sinaimg.cn/large/006tNc79gy1fdkqyzihmwj30xw0j277d.jpg)

Tensors are datas on the edge.

- How to get the value of a.

  - Create a session and assign it to variable sess.
  - Withen the session, evaluate the graph to fetch the value of a.

  ```python
  import tensorflow as tf
  a = tf.add(3,5)
  sess = tf.Session()
  print less.run(a)
  sess.close()
  ```

- tf.Session(): A Session object encapsulates the environment in which Operation objects are executed, and Tensor objects are evaluated.

- By using Session, we can calculate result with many subgraphs in a graphs. It is not wise to build more than one graph.

  - Multiple graphs need multiple sessions, each will try to use all available resources.

  - Can't pass data between them without passing them through python/numpy, which doesn't work in distributed.

  - ​

    ​