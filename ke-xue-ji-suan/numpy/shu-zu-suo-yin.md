### 数组索引

注意：切片与python列表类似，可以切割numpy数组。

由于数组可能是多维的，因此必须为数组的每个维指定一个切片：

```
# -*- coding: utf-8 -*-
"""
Created on Tue Oct 16 19:08:10 2018

@author: tokimeki
"""

import numpy as np

# 创建一个3x4的二维数组
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]

a = np.array([
        [1,2,3,4],
        [5,6,7,8],
        [9,10,11,12]
        ])

# 分割前两行并且同时分割第一列和第二列出来
b = a[:2,1:3]

print(b)

# 数组的一个片段是对相同数据的视图，因此需要对其进行修改
# 将修改原始数组
print(a[0, 1])   # 2
b[0, 0] = 77     # b [0,0]是与[0,1]相同的数据
print(a[0, 1])   # 77
```

可以将整数索引与切片索引混合使用

```
# -*- coding: utf-8 -*-
"""
Created on Tue Oct 16 22:34:06 2018

@author: tokimeki
"""

import numpy as np

# 创建一个3x4的二维数组
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

# 访问数组中间行中的数据的两种方法
# 将整数索引与切片混合生成低秩数组
# 使用切片产生与原始数组相同的秩的数组
row_r1 = a[1,:] # 创建一个一维数组
row_r2 = a[1:2,:] # 创建一个二维数组

print(row_r1) # [5 6 7 8]------(4,)
print(row_r2) # [[5 6 7 8]]----(1,4)


# 列
col_r1 = a[:,1]
col_r2 = a[:,1:2]
print(col_r1,col_r1.shape) #[ 2  6 10] (3,)
print(col_r2,col_r2.shape) #[[ 2]
                           # [ 6]
                           # [10]] (3, 1)
```

整数数组索引： 使用切片索引到numpy数组时，生成的数组视图将始终是原始数组的子数组。相反，整数数组索引允许您使用另一个数组中的数据构造任意数组。

```
# -*- coding: utf-8 -*-
"""
Created on Tue Oct 16 22:45:22 2018

@author: tokimeki
"""

import numpy as np

a = np.array([[1,2],[3,4],[5,6]])

# 整数索引
# 返回一位数组[a[0,0],a[0,1],a[1,1]]
print(a[[0,0,1],[0,1,1]]) # [1 2 4]

# 等效
print(np.array([a[0,0],a[0,1],a[1,1]])) # [1 2 4]

print(a[[0,0],[1,1]]) # [2 2]
print(np.array([a[0,1],a[0,1]])) # [2 2]



x = np.array([[ 0,  1,  2],
            [ 3,  4,  5],
            [ 6,  7,  8],
           [ 9, 10, 11]])
rows = np.array([[0, 0],[3, 3]], dtype=np.intp)
columns = np.array([[0, 2],[0, 2]], dtype=np.intp)
# [0,0],[0,2],[3,0],[3,2]
print(x[rows,columns])
# [[ 0  2]
#  [ 9 11]]

rows = np.array([0,3], dtype=np.intp)
columns = np.array([0,2], dtype=np.intp)
# [0,0],[0,2],[3,0],[3,2]
print(x[np.ix_(rows,columns)])
# [[ 0  2]
#  [ 9 11]]
```

整数数组索引的一个有用技巧是从矩阵的每一行中选择或改变一个元素

```
import numpy as np

a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
print(a)  # prints "array([[ 1,  2,  3],
          #                [ 4,  5,  6],
          #                [ 7,  8,  9],
          #                [10, 11, 12]])"


b = np.array([0, 2, 0, 1])
print(a[np.arange(4), b])  # Prints "[ 1  6  7 11]"


a[np.arange(4), b] += 10
print(a)  # prints "array([[11,  2,  3],
          #                [ 4,  5, 16],
          #                [17,  8,  9],
          #                [10, 21, 12]])
```

布尔数组索引： 布尔数组索引允许您选择数组的任意元素

```
# -*- coding: utf-8 -*-
"""
Created on Tue Oct 16 23:10:00 2018

@author: tokimeki
"""

import numpy as np

a = np.array([[1,2],[3,4],[5,6]])

bool_idx = (a>2) # 寻找到大于2的元素，并返回true，否者返回false
print(bool_idx)  # [[False False]
                 # [ True  True]
                 # [ True  True]]

# 使用返回的bool数组，来返回一个bool值为true的数组
print(a[bool_idx]) # [3 4 5 6]

# 简介的实例
print(a[a>2]) # [3 4 5 6]
```

### 



