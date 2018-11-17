### 语法

```
__import__(name[, globals[, locals[, fromlist[, level]]]])
```

### 作用

用于动态加载类和函数,如果一个模块经常变化就可以使用 \_\_import\_\_\(\) 来动态载入

### 参数

* x:int类型的数字

### 实例

以下实例展示了 \_\_import\_\_ 的使用方法：

##### a.py 文件代码：

```
import os  
 
print ('在 a.py 文件中 %s' % id(os))
test.py 文件代码：
#!/usr/bin/env python    
#encoding: utf-8  
 
import sys  
__import__('a')        # 导入 a.py 模块
执行 test.py 文件，输出结果为：
```

##### test.py 文件代码：

```
import sys  
__import__('a')        # 导入 a.py 模块
```

执行 test.py 文件，输出结果为：

```
在 a.py 文件中 4394716136
```



