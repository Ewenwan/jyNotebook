### 数据类型

```
import numpy as np

x = np.array([1, 2])   
print(x.dtype)         # int64

x = np.array([1.0, 2.0])   
print(x.dtype)             # float64

x = np.array([1, 2], dtype=np.int64)   # 强制使用特定的数据类型
print(x.dtype)                         # int64
```

内置Python类型

> 用于生成`dtype`对象时，有几种python类型等效于相应的数组标量：
>
> | `int` | `int_` |
> | :--- | :--- |
> | `bool` | `bool_` |
> | `float` | `float_` |
> | `complex` | `cfloat` |
> | `bytes` | `bytes_` |
> | `str` | `bytes_`（Python2）或`unicode_`（Python3） |
> | `unicode` | `unicode_` |
> | `buffer` | `void` |
> | （所有其他人） | `object_` |



