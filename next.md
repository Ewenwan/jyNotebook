### 语法

```
next(iterator[, default])
```

### 作用

返回迭代器的下一个项目

### 参数

* iterator -- 可迭代对象

* default -- 可选，用于设置在没有下一个元素时返回该默认值，如果不设置，又没有下一个元素则会触发 StopIteration 异常

### 实例

```
>>> # 首先获得Iterator对象:
... it = iter([1, 2, 3, 4, 5])
>>> # 循环:
... while True:
...     try:
...         # 获得下一个值:
...         x = next(it)
...         print(x)
...     except StopIteration:
...         # 遇到StopIteration就退出循环
...         break
...
1
2
3
4
5
```



