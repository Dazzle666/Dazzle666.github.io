---
layout:     post
title:      "初识tensorflow Cookbook chapter2（一）"
subtitle:   "图表运算原理"
date:       2018-05-21 15:25:00
author:     "SethD"
header-img: "img/post-bg-dubai.jpg"
tags:
    - TensorFlow
    - 图形运算
    - AI
---

# 图表运算原理
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

> 创建tensors
```Python
# 创建数据填充占位符
x_vals = np.array([1., 3., 5., 7., 9.])

# 创建TensorFlow占位符
x_data = tf.placeholder(tf.float32)

# 乘数
m = tf.constant(3.)
```

> 我们遍历输入参数，并且输出每个输入的乘法运算

```Python
# 乘法
prod = tf.multiply(x_data, m)
for x_val in x_vals:
    print(sess.run(prod, feed_dict={x_data: x_val}))
```

# 输出图表到tensorboard
```Python
# 乘法
merged = tf.summary.merge_all(key='summaries')
if not os.path.exists('tensorboard_logs/'):
    os.makedirs('tensorboard_logs/')

my_writer = tf.summary.FileWriter('tensorboard_logs/', sess.graph)
```