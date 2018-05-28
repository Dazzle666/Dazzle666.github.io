---
layout:     post
title:      "初识tensorflow Cookbook chapter2（三）"
subtitle:   "分层嵌套运算的使用"
date:       2018-05-22 15:25:00
author:     "SethD"
header-img: "img/post-bg-thinker.jpg"
tags:
    - TensorFlow
    - 分层嵌套运算的应用
    - AI
---

# 分层嵌套运算的应用
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
这里我们创建一个4x4像素的小图片并且通过分层嵌套运算增值图片
```Python
# Create a small random 'image' of size 4x4
x_shape = [1, 4, 4, 1]
x_val = np.random.uniform(size=x_shape)
```

# 创建数据占位符
```Python
x_data = tf.placeholder(tf.float32, shape=x_shape)
```

# 第一层：移动窗口（回旋）
> 我们第一层运算是两步2x2空间移动窗口（在长宽两个方向）
  移动窗口平均，过滤值将全部是0.25
  
 ```Python
# Create a layer that takes a spatial moving window average
# Our window will be 2x2 with a stride of 2 for height and width
# The filter value will be 0.25 because we want the average of the 2x2 window
my_filter = tf.constant(0.25, shape=[2, 2, 1, 1])
my_strides = [1, 2, 2, 1]
mov_avg_layer= tf.nn.conv2d(x_data, my_filter, my_strides,
                            padding='SAME', name='Moving_Avg_Window')
```

# 第二层：定制
> 我们的第二层将会是自定义层。给定一个输入，x，这一层变平x和运算sigmoid（Ax+b）。这里的A和b为预设常数。
  我们之后添加自定义层到名为"Custom_Layer"图表.这使得我们可以稍后通过tensorboard来肉眼观察。
  
   ```Python
# Define a custom layer which will be sigmoid(Ax+b) where
# x is a 2x2 matrix and A and b are 2x2 matrices
def custom_layer(input_matrix):
    input_matrix_sqeezed = tf.squeeze(input_matrix)
    A = tf.constant([[1., 2.], [-1., 3.]])
    b = tf.constant(1., shape=[2, 2])
    temp1 = tf.matmul(A, input_matrix_sqeezed)
    temp = tf.add(temp1, b) # Ax + b
    return(tf.sigmoid(temp))

# Add custom layer to graph
with tf.name_scope('Custom_Layer') as scope:
    custom_layer1 = custom_layer(mov_avg_layer)
```

# 运行输出结果

> 输出应该是一个2x2的数组，但是size为（1,2,2,1）
   ```Python
print(sess.run(mov_avg_layer, feed_dict={x_data: x_val}))
```

> 在自定义操作之后，现在大小为2x2（挤压大小1 dims），
   ```Python
print(sess.run(custom_layer1, feed_dict={x_data: x_val}))
```

> 存储 纪要到tensorboard试图
   ```Python
merged = tf.summary.merge_all(key='summaries')

if not os.path.exists('tensorboard_logs/'):
    os.makedirs('tensorboard_logs/')

my_writer = tf.summary.FileWriter('tensorboard_logs/', sess.graph)
```