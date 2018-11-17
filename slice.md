### 语法

```
slice(stop)
slice(start, stop[, step])
```

### 作用

实现切片对象，主要用在切片操作函数里的参数传递

### 参数

* start: 起始位置

* stop: 结束位置

* step:间距

### 实例

```
>>> result = slice(2) # 设置街区2个元素的切片
>>> result
slice(None, 2, None)
>>> value = list(range(10))
>>> value
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> value[result] # 截取2个元素
[0, 1]
```



