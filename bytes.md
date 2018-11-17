### 语法

```
bytes([source[, encoding[, errors]]])
```

### 作用

返回一个新的 bytes 对象，该对象是一个 0 &lt;= x &lt; 256 区间内的整数不可变序列。它是 bytearray 的不可变版本

### 参数

* 如果 source 为整数，则返回一个长度为 source 的初始化数组；

* 如果 source 为字符串，则按照指定的 encoding 将字符串转换为字节序列；

* 如果 source 为可迭代类型，则元素必须为\[0 ,255\] 中的整数；

* 如果 source 为与 buffer 接口一致的对象，则此对象也可以被用于初始化 bytearray。
* 如果没有输入任何参数，默认就是初始化数组为0个元素。

### 实例

```
>>>a = bytes([1,2,3,4])
>>> a
b'\x01\x02\x03\x04'
>>> type(a)
<class 'bytes'>

>>> a = bytes('hello','ascii')

>>> a
b'hello'
>>> type(a)
<class 'bytes'>
```



