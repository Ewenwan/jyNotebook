### 数组

numpy数组是一个值网格，所有类型都相同，并由非负整数元组索引。维数是数组的排名 ; 数组的形状是一个整数元组，给出了每个维度的数组大小

* 初始化numpy数组，并访问元素

```
import numpy as np

a = np.array([1,2,3]) # 创建一个数组
print(type(a))        # <class 'numpy.ndarray'>
print(a.shape)        # 形状，维度
print(a[0],a[1],a[2]) # 1,2,3
a[0] = 5
print(a)              # [5,2,3]


b = np.array([        # 创建一个二维数组
        [1,2,3],
        [4,5,6],
        ])
print(b.shape)                #(2, 3)
print(b[0,0],b[0,1],b[1,0])   #1 2 4
```

* 其他创建数组的函数

```
# -*- coding: utf-8 -*-
"""
Created on Tue Oct 16 18:57:21 2018

@author: tokimeki
"""

import numpy as np

a = np.zeros((2,2)) # 创建2x2一个全是0的数组
print(a)
# [[0. 0.]
#  [0. 0.]]

b = np.ones((1,2)) # 创建1x2一个全书1的数组
print(b)
# [[1. 1.]]

c = np.full((2,2),7) # 创建一个2x2全是7的不变的数组
print(c)
# [[7 7]
# [7 7]]

d = np.eye(2) # 创建一个2x2的单位矩阵
print(d)
# [[1. 0.]
# [0. 1.]]

e = np.random.random((2,3)) # 创建一个2x3随机生成值组成的数组
print(e)
# [[0.20204016 0.90410974 0.20027459]
# [0.89359858 0.5981336  0.26197809]]


f = np.linspace(1,4,6) #将创建具有指定数量元素的数组，并在指定的开始值和结束值之间平均间隔
print(f)
# [1.  1.6 2.2 2.8 3.4 4. ]
```

### 



