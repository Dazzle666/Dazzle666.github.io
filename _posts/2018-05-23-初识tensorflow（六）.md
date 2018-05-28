---
layout:     post
title:      "初识tensorflow（六）"
subtitle:   "激活函数"
date:       2018-05-22 15:25:00
author:     "SethD"
header-img: "img/post-bg-thinker.jpg"
tags:
    - TensorFlow
    - 激活函数
    - AI
---

# 激活函数
> 这个函数介绍了TensorFlow的激活函数

```Python
import matplotlib.pylot as plt
import numpy as np
import tensorflow as tf
from tensorflow.python.framework import ops
ops.reset_default_graph()
sess = tf.Session()
```

# 初始化X绘图范围值
```Python
x_vals = np.linspace(start = -10.,stop = 10.,num = 100)
```

# 激活函数：
> ReLU 激活
```Python
print(sess.run(tf.nn.relu([-3., 3., 10.])))
y_relu = sess.run(tf.nn.relu(x_vals))
```

> ReLU-6 激活
```Python
print(sess.run(tf.nn.relu6([-3., 3., 10.])))
y_relu6 = sess.run(tf.nn.relu6(x_vals))
```

> Sigmoid激活
```Python
print(sess.run(tf.nn.sigmoid([-1., 0., 1.])))
y_sigmoid = sess.run(tf.nn.sigmoid(x_vals))
```

> Hyper Tangent激活
```Python
print(sess.run(tf.nn.tanh([-1., 0., 1.])))
y_tanh = sess.run(tf.nn.tanh(x_vals))
```

> softsign 激活
```Python
print(sess.run(tf.nn.softsign([-1., 0., 1.])))
y_softsign = sess.run(tf.nn.softsign(x_vals))
```

> Softplus 激活
```Python
print(sess.run(tf.nn.softplus([-1., 0., 1.])))
y_softplus = sess.run(tf.nn.softplus(x_vals))
```

> Exponential linear 激活
```Python
print(sess.run(tf.nn.elu([-1., 0., 1.])))
y_elu = sess.run(tf.nn.elu(x_vals))
```

# 绘制不同的函数
```Python
plt.plot(x_vals, y_softplus, 'r--', label='Softplus', linewidth=2)
plt.plot(x_vals, y_relu, 'b:', label='ReLU', linewidth=2)
plt.plot(x_vals, y_relu6, 'g-.', label='ReLU6', linewidth=2)
plt.plot(x_vals, y_elu, 'k-', label='ExpLU', linewidth=0.5)
plt.ylim([-1.5,7])
plt.legend(loc='upper left')
plt.show()

plt.plot(x_vals, y_sigmoid, 'r--', label='Sigmoid', linewidth=2)
plt.plot(x_vals, y_tanh, 'b:', label='Tanh', linewidth=2)
plt.plot(x_vals, y_softsign, 'g-.', label='Softsign', linewidth=2)
plt.ylim([-2,2])
plt.legend(loc='upper left')
plt.show()
```