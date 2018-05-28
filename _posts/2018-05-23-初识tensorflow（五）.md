---
layout:     post
title:      "初识tensorflow（五）"
subtitle:   "声明运算/操作"
date:       2018-05-22 15:25:00
author:     "SethD"
header-img: "img/post-bg-thinker.jpg"
tags:
    - TensorFlow
    - 操作/运算
    - AI
---

# 操作/运算
> 这个函数包含了TensorFlow中的多种运算
  声明操作

```Python
import matplotlib.pylot as plt
import numpy as np
import tensorflow as tf
from tensorflow.python.framework import ops
ops.reset_default_graph()
```

> 通过tf.Session开始一个图表session
	
```Python
sess = tf.Session()
```

# 算术运算
> ## TensorFlow有多种类型的算术运算函数，这里我们主要着重区分div(),truediv()和floordiv().
> 1. div():整数除法（类似于Python中的//）
> 2. truediv():会把整数转换成浮点类型
> 3. floordiv():float类型的div（）（我理解为按div（）函数进行运算，然后将结果返回为float类型的）
```Python
print(sess.run(tf.div(3,4)))
print(sess.run(tf.truediv(3,4)))
print(sess.run(tf.floordiv(3.0,4.0)))
```

> ## 取余运算：
```Python
print(sess.run(tf.mod(22.0,5.0)))
```

> ## 叉乘运算
叉乘运算就是求同时垂直于两个向量的向量，并且向量的模等于两向量模长乘积乘上向量夹角正弦值。
几何意义为两向量所构成平行四边形的面积。
```Python
print(sess.run(tf.cross([1.,0.,0.],[0.,1.,0.])))
```
值为[0.,0.,1.]

# 三角函数
> sine、cosine 和 tangent
```Python
print(sess.run(tf.sin(3.1416)))
print(sess.run(tf.cos(3.1416)))
print(sess.run(tf.div(tf.sin(3.1416/4.),tf.cos(3.1416/4.))))
```

# 自定义运算
可以创建多项式函数：
f(x) = 3 * x^2 - x + 10
```Python
test_nums = range(15)

def custom_polymomial(x_val):
	#Return 3x^2 - x + 10
	return(tf.sub(3 * tf.square(x_val),x_val) + 10)
	
print(sess.run(custom_polymomial(11)))
```
> 我们通过输入数组会得到：
```Python
#（0-15的数组依次赋值给该自定义常数项）
expected_output = [3*x*x-x+10 for x in test_nums]
print(expected_output)
```

> TensorFlow自定义函数输出
```Python
for num in test_nums:
	print(sess.run(custom_polymomial(num)))
```
对比输出结果相同。

