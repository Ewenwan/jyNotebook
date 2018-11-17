### 语法

```
hasattr(object, name)
```

### 作用

判断对象是否包含对应的属性

### 参数

* object:对象

* name:字符串，属性名

### 实例

```
>>> class A:
...     a=1
...     b=2
...
>>> test = A()
>>> hasattr(test,'a')
True
>>> hasattr(test,'b')
True
>>> hasattr(test,'c')
False
>>> hasattr(test,'d')
False
```



