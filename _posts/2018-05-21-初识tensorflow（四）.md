---
layout:     post
title:      "初识tensorflow（四）"
subtitle:   "矩阵和矩阵运算"
date:       2018-05-21 15:25:00
author:     "SethD"
header-img: "img/post-bg-dubai.jpg"
tags:
    - TensorFlow
    - 矩阵
    - 矩阵运算
    - AI
---

# 矩阵
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

> 声明矩阵
识别矩阵
```Python
identity_matrix = tf.diag([1.0,1.0,1.0])
print(sess.run(identity_matrix))
```

2x3随机范数矩阵：
```Python
A = tf.truncated_normal([2,3])
print(sess.run(A))
```

2x3常数矩阵：
```Python
B = tf.fill([2,3],5.0)
print(sess.run(B))
```

3x2随机统一矩阵
```Python
C = tf.random_uniform([3,2])
print(sess.run(C))
```

通过np对象创建矩阵
```Python
D = tf.convert_to_tensor(np.array([[1., 2., 3.], [-3., -7., -1.], [0., 5., -2.]]))
print(sess.run(D))
```

# 矩阵运算
> 矩阵加、减法
```Python
print(sess.run(A+B))
print(sess.run(B-B))
```

> 矩阵乘法
```Python
print(sess.run(tf.matmul(B, identity_matrix)))
```

> 矩阵转置运算
```Python
print(sess.run(tf.transpose(C)))
```

> 矩阵行列式求值
```Python
print(sess.run(tf.matrix_determinant(D)))
```

> 矩阵逆运算
```Python
print(sess.run(tf.matrix_inverse(D)))
```

> Cholesky分解
```Python
print(sess.run(tf.cholesky(identity_matrix)))
```

>特征值和特征向量：我们使用tf.self_adjoint_eig()函数，返回两个对象，第一个是数组特征值，第二个是矩阵特征向量。
```Python
eigenvalues, eigenvectors = sess.run(tf.self_adjoint_eig(D))
print(eigenvalues)
print(eigenvectors)
```