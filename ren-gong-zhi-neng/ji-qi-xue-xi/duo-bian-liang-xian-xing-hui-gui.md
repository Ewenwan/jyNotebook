```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib
```

In \[2\]:

```
train_data = pd.read_csv("examples.csv")
```

In \[3\]:

```
train_data = pd.DataFrame(train_data)
```

In \[4\]:

```
train_data.insert(0,"",np.ones((4,1),dtype=int))
train_data
```

Out\[4\]:

|  |  | size | bedrooms | floors | years | price |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 1 | 2104 | 5 | 1 | 45 | 460 |
| 1 | 1 | 1416 | 3 | 2 | 40 | 232 |
| 2 | 1 | 1534 | 3 | 2 | 30 | 315 |
| 3 | 1 | 852 | 2 | 1 | 36 | 178 |

In \[5\]:

```
train_data.describe()
```

Out\[5\]:

|  |  | size | bedrooms | floors | years | price |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| count | 4.0 | 4.00000 | 4.000000 | 4.00000 | 4.000000 | 4.000000 |
| mean | 1.0 | 1476.50000 | 3.250000 | 1.50000 | 37.750000 | 296.250000 |
| std | 0.0 | 513.39491 | 1.258306 | 0.57735 | 6.344289 | 122.850519 |
| min | 1.0 | 852.00000 | 2.000000 | 1.00000 | 30.000000 | 178.000000 |
| 25% | 1.0 | 1275.00000 | 2.750000 | 1.00000 | 34.500000 | 218.500000 |
| 50% | 1.0 | 1475.00000 | 3.000000 | 1.50000 | 38.000000 | 273.500000 |
| 75% | 1.0 | 1676.50000 | 3.500000 | 2.00000 | 41.250000 | 351.250000 |
| max | 1.0 | 2104.00000 | 5.000000 | 2.00000 | 45.000000 | 460.000000 |

In \[6\]:

```
data = np.array(train_data)
data
```

Out\[6\]:

```
array([[   1, 2104,    5,    1,   45,  460],
       [   1, 1416,    3,    2,   40,  232],
       [   1, 1534,    3,    2,   30,  315],
       [   1,  852,    2,    1,   36,  178]], dtype=int64)
```

In \[7\]:

```
X = data[:,:-1]
X
```

Out\[7\]:

```
array([[   1, 2104,    5,    1,   45],
       [   1, 1416,    3,    2,   40],
       [   1, 1534,    3,    2,   30],
       [   1,  852,    2,    1,   36]], dtype=int64)
```

In \[8\]:

```
y = data[:,-1]
y
```

Out\[8\]:

```
array([460, 232, 315, 178], dtype=int64)
```

In \[10\]:

```
# the_ta = np.linalg.inv(X.T.dot(X)).dot(X.T).dot(y)
#X.T@X等价于X.T.dot(X)

# np.linalg.inv(array) ==> 求解逆矩阵
# np.linalg.pinv(array) ==> 在不可逆矩阵情况下，求解伪逆矩阵

# array.T ==> 转置矩阵

# np.dot(arr1,arr2) <==> arr1.dot(arr2) ==> 矩阵乘

# np.linalg.det(array) ==> 求矩阵的行列式

# numpy.linalg.eig(array) ==> 想要计算奇异值和右奇异值
#                       返回值：
#                       w：特征值。每个特征值根据它的多重性重复。这个数组将是复杂类型，
#                          除非虚数部分为0。当传进的参数a是实数时，得到的特征值是实数。
#                       v：特征向量。

# np.mat()是将序列转为np的二维数组

# np.transpose()是将数组转置

# solve 求出向量 x，使 Ax = b
# 内部使用 np.dot(A.I, b) 来计算
# 所以 A 不可逆时报错
# x = np.linalg.solve(A, b)


the_ta = np.linalg.inv(X.T@X)@X.T@y
the_ta
```

Out\[10\]:

```
array([-3497.84375   ,    -6.49743652,  2550.65625   ,  1825.109375  ,
         -57.70019531])
```



