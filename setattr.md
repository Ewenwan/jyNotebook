### 语法

```
setattr(object, name, value)
```

### 作用

setattr\(\) 函数对应函数 getattr\(\)，用于设置属性值，该属性必须存在

### 参数

* object:对象

* name:字符串，对象属性

* value:属性值

### 实例

```
>>> class test(object):
...     number = 1
...
>>> a = test()
>>> getattr(a,'number')
1
>>> setattr(a,'number',40)
>>> a.number
40
```



