### 数学

基本数学函数在数组上以元素方式运行，既可以作为运算符重载，也可以作为numpy模块中的函数

```
# -*- coding: utf-8 -*-
"""
Created on Wed Oct 17 19:29:19 2018


@author: tokimeki
"""


import numpy as np


x = np.array([
        [1,2],
        [3,4]
        ],dtype=np.float64)
# [[1. 2.]
#  [3. 4.]]


y = np.array([
        [5,6],
        [7,8]
        ],dtype=np.float64)
# [[5. 6.]
#  [7. 8.]]


# 矩阵加法
print(x+y)
print(np.add(x,y))
# [[ 6.  8.]
# [10. 12.]]




# 矩阵减法
print(x-y)
print(np.subtract(x,y))
# [[-4. -4.]
#  [-4. -4.]]




# 矩阵乘法
print(x*y)
print(np.multiply(x,y))
# [[ 5. 12.]
#  [21. 32.]]


# 矩阵除法
print(x/y)
print(np.divide(x,y))
# [[0.2        0.33333333]
#  [0.42857143 0.5       ]]




# 矩阵平方
print(np.sqrt(x))
# [[1.         1.41421356]
#  [1.73205081 2.        ]]




# dot函数来计算向量的内积




x = np.array([
        [1,2],
        [3,4]
        ])


y = np.array([
        [5,6],
        [7,8]
        ])


v = np.array([9,10])
w = np.array([11,12])


# 如果处理的是一维数组，则得到的是两数组的內积
# 9*11 + 10*12=120+99=219
print(v.dot(w)) # 219
print(np.dot(v,w))


# 如果是二维数组（矩阵）之间的运算，则得到的是矩阵积
# 1*5+2*7=19
# 1*6+2*8=22
# 3*5+4*7=43
# 3*6+4*8=50
print(x.dot(y))
# [[19 22]
#  [43 50]]
```

* sum\(\)函数方法

```
# -*- coding: utf-8 -*-
"""
Created on Wed Oct 17 20:01:47 2018


@author: tokimeki
"""


import numpy as np


x = np.array([
        [1,2],
        [3,4]
        ])


# 计算所有元素的总和
print(np.sum(x)) # 10


# 计算每一列的总和
print(np.sum(x,axis=0)) # [4 6]


# 计算每一行的总和
print(np.sum(x,axis=1)) # [3 7]
```

转置矩阵

```
# 转置，但是一位数组的转置无效
a = np.array([
        [1,2],
        [3,4]
        ])
print(a)
# [[1 2]
# [3 4]]


print(a.T)
# [[1 3]
# [2 4]]
```





