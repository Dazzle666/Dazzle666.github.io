---
layout:     post
title:      "初识tensorflow Cookbook chapter2（二）"
subtitle:   "分层嵌套运算"
date:       2018-05-22 15:25:00
author:     "SethD"
header-img: "img/post-bg-dubai.jpg"
tags:
    - TensorFlow
    - 分层嵌套运算
    - AI
---

# 分层嵌套运算
> 首先加载必要的库并重置图表计算session

```Python
import os
import matplotlib.pyplot as plt
import numpy as np
import tensorflow as tf
from tensorflow.python.framework import ops
ops.reset_default_graph()
```

> 开始一个运算session
```Python
sess = tf.Session()
```

> 创建tensors，常量和占位符

填入一个数组到占位符中（注意维度的协议）。我们之后声明一些图表常量用于之后的运算。
```Python
# Create data to feed in
my_array = np.array([[1., 3., 5., 7., 9.],
                   [-2., 0., 2., 4., 6.],
                   [-6., -3., 0., 3., 6.]])
# Duplicate the array for having two inputs
x_vals = np.array([my_array, my_array + 1])
# Declare the placeholder
x_data = tf.placeholder(tf.float32, shape=(3, 5))
# Declare constants for operations
m1 = tf.constant([[1.],[0.],[-1.],[2.],[4.]])
m2 = tf.constant([[2.]])
a1 = tf.constant([[10.]])
```

# 声明操作
> 我们以矩阵乘法开始（A[3x5]*m1[5x1]）= prod1[3x1]
```Python
# 1st Operation Layer = Multiplication
prod1 = tf.matmul(x_data, m1)
```

> 第二层运算是prod1[3x1]和m2[1x1]乘法运算,运算结果为prod2[3x1]
```Python
# 2nd Operation Layer = Multiplication
prod2 = tf.matmul(prod1, m2)
```
> 第三层运算是矩阵prod2[3x1]和a1[1x1]加和运算.用到了TensorFlow广播。
```Python
# 3rd Operation Layer = Addition
add1 = tf.add(prod2, a1)
```

# 评估和打印输出
```Python
for x_val in x_vals:
    print(sess.run(add1, feed_dict={x_data: x_val}))
```

# 创建和格式化tensorboard输出到试图
```Python
merged = tf.summary.merge_all(key='summaries')

if not os.path.exists('tensorboard_logs/'):
    os.makedirs('tensorboard_logs/')

my_writer = tf.summary.FileWriter('tensorboard_logs/', sess.graph)
```
