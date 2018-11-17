Python3 布尔类型（bool）是一种内置数据类型，具有两个值:True和False

| 数据类型 | 满足true的值 | 满足false的值 |
| :--- | :--- | :--- |
| 数字类型 | 除0以外的任意值 | 0 |
| 字符串类型 | 除空字符串（""）以外的任意字符串 | 空字符串（""） |

```
>>> bool("")
False
>>> bool(0)
False
>>> bool(1)
True
>>> bool("1")
True
>>> a = 0
>>> if a:
...     print("为真")
... else:
...     print("为假")
...
为假
```



