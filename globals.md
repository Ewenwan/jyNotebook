### 语法

```
globals()
```

### 作用

globals\(\)函数会以字典类型返回当前位置的全部全局变量

### 实例

```
>>> name = "angle"
>>> globals() # 字典中会有一个name变量，值为"angle"
                # globals 函数返回一个全局变量的字典，包括所有导入的变量
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'str': 'for i in range(5):\n\tprint("value:{}".format(i))\n', 'str_utf': b'\xe5\xa4\xa9\xe4\xbd\xbf', 'str_gbk': b'\xcc\xec\xca\xb9', 'suffix': 'jc', 'str2': 'llo', 'intab': 'abcde', 'outtab': '12345', 'tab': {97: 49, 98: 50, 99: 51, 100: 52, 101: 53}, 'str1': 'adaAd', 'test': <class '__main__.test'>, 'a': ['a', 'b', 'c', 'd'], 'i': 4, 'element': 'd', 'name': 'angle'}
```



