### 语法

```
dir([object])
```

### 作用

不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法\_\_dir\_\_\(\)，该方法将被调用。如果参数不包含\_\_dir\_\_\(\)，该方法将最大限度地收集参数信息

### 参数

* object:对象、变量、类型。

### 实例

```
>>> dir()  # 获得当前模块的属性列表
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'intab', 'outtab', 'str', 'str1', 'str2', 'str_gbk', 'str_utf', 'suffix', 'tab', 'test']
>>> dir(list) # 查看列表的方法
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```



