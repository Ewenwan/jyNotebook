### 语法

```
memoryview(object)
```

### 作用

返回给定参数的内存查看对象\(Momory view\)。

所谓内存查看对象，是指对支持缓冲区协议的数据进行包装，在不需要复制对象基础上允许Python代码访问

### 参数

* object:对象

### 实例

```
>>> v = memoryview(bytearray('abcdef','utf8'))
>>> v[1]
98
>>> v[1:4]
<memory at 0x000001BB7C92C588>
>>> v[1:4].tobytes()
b'bcd'
```



