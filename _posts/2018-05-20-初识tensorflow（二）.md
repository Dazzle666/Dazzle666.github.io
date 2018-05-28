---
layout:     post
title:      "初识tensorflow（二）"
subtitle:   "Tensor的创建"
date:       2018-05-20 15:25:00
author:     "SethD"
header-img: "img/post-bg-thinker.jpg"
tags:
    - TensorFlow
    - Tensors
    - AI
---

> 首先加载TensorFlow并重置图表计算

```Python
import tensorflow as tf
from tensorflow.python.framework import ops
ops.reset_default_graph()
```

> 通过tf.Session开始一个图表session
	
```Python
sess = tf.Session()
```

> 创建Tensors
TensorFlow建立了一个用来创建tensors以使用变量的函数。例如，我们可以如下，通过tr.zeros()函数创建一个预设全为零的结构。


```Python
my_tensor = tf.zeros([1,20])
```

我们可以通过调用session的run()函数来评估tensors

```Python
sess.run(my_tensor)
```

TensorFlow运算法则需要指导那些对象是变量或是常量。
现在我们通过tensorflow函数tf.Variable()创建一个变量.


```Python
my_var = tf.Variable(tf.zeros([1,20]))
```

注意，你无法运行sess.run(my_var),它会报错，因为TensorFlow随着运算图表运行，我们必须创建一个变量初始化操作用以评估变量。之后你会了解更多。在此处，我们能一次性初始化一个变量,通过调用变量方法my_var.initalizer

```Python
sess.run(my_var.initalizer)
sess.run(my_var)
```

让我们开始先通过声明行列大小来创建特定结构的变量

```Python
row_dim = 2
col_dim = 3
```

下面是全零和全一的初始化后的变量
```Python
zero_var = tf.Variable(tf.zero([row_dim,col_dim]))
ones_var = tf.Variable(tf.ones([row_dim,col_dim]))
```

接下来，我们可以调用初始化构造器方法在我们的变量，并且评估它们的内容。

```Python
sess.run(zero_var.initializer)
sess.run(ones_var.initializer)
print(sess.run(zero_var))
print(sess.run(ones_var))
```

[[ 0.  0.  0.]
 [ 0.  0.  0.]]
[[ 1.  1.  1.]
 [ 1.  1.  1.]]
 
 
 > 用常量填充tensor
 
 下面是用常量填充tensor的方法
 ```Python
fill_var = tf.Variable(tf.fill([row_dim, col_dim], -1))
sess.run(fill_var.initializer)
print(sess.run(fill_var))
```

也可以通过常量数组或列表来填充

 ```Python
# Create a variable from a constant
const_var = tf.Variable(tf.constant([8, 6, 7, 5, 3, 0, 9]))
# This can also be used to fill an array:
const_fill_var = tf.Variable(tf.constant(-1, shape=[row_dim, col_dim]))

sess.run(const_var.initializer)
sess.run(const_fill_var.initializer)

print(sess.run(const_var))
print(sess.run(const_fill_var))
```

[8 6 7 5 3 0 9]
[[-1 -1 -1]
 [-1 -1 -1]]
 
 
 