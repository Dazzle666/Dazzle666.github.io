---
layout:     post
title:      "初识tensorflow（三）"
subtitle:   "占位符"
date:       2018-05-21 15:25:00
author:     "SethD"
header-img: "img/post-bg-thinker.jpg"
tags:
    - TensorFlow
    - 占位符
    - AI
---

> 首先加载必要的库并重置图表计算session

```Python
import numpy as np
import tensorflow as tf
from tensorflow.python.framework import ops
ops.reset_default_graph()
```

> 通过tf.Session开始一个图表session
	
```Python
sess = tf.Session()
```

> 声明一个占位符
我们通过TensorFlow的tf.placeholder()函数来声明一个占位符，数据类型为tf.float32,矩阵体型为（4,4）。注意这个模型可以为数组或是一个列表[4,4]

```Python
x = tf.placeholder(tf.float32,shape=(4,4))
```

为了阐释如何使用一个占位符，我们为它创建一个源数据，并且在tensorboard上进行假设。

注意feed_dict的用法，它可以让我们把x的值填入到运算图表中

 
 ```Python
rand_array = np.random.rand(4,4)

y = tf.identify(x)

print(sess.run(y,feed_dict={x: rand_array}))

```

在tensorboard中模拟结合之前的总结，卸载一个log文件中
 ```Python
merged = tf.summary.merge_all()
writer = tf.summary.FileWriter("/tmp/variable_logs", sess.graph)
```

在anaconda prompt中跑如下命令
tensorboard --logdir=/tmp

这将告诉我们通过chrome模拟图表计算的地址：默认为：http://0.0.0.0:6006/



