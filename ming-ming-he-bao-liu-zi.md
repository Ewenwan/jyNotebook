# 命名规范

### 应该避免的名称

以下的命名应该尽量避免:

* 单字符名称, 除了计数器和迭代器

```
s = "hello world"
```

* 包/模块名中的连字符\(-\)

```
# 错误的包名
# 引用文件 html-parser.py
import html-parser

# 正确的写法
# 文件名应为 html_parser.py
import html_parser
```

* 双下划线开头并结尾的名称\(Python保留, 例如\_\_init\_\_\)

* 应避免使用小写字母l\(L\)，大写字母O\(o\)或I\(i\)单独作为一个变量的名称，以区分数字1和0

* 当参数名称和Python保留字冲突，可在最后添加一个下划线，而不是使用缩写或自造的词

```
# 如果变量名和python保留字冲突，则在末尾添加下划线
# 切记不要自己造词，或者使用缩写

str_ = "hello world!"
print_(str_)
```

### 命名约定

* 模块

  * 模块尽量使用小写命名，首字母保持小写，尽量不要用下划线\(除非多个单词，且数量不多的情况\)

* 类名

  * 类名使用驼峰\(CamelCase\)命名风格，首字母大写，私有类可用一个下划线开头

```
class OurHome():
    pass
```

* 函数
  * 函数名一律小写，如有多个单词，用下划线隔开
  * 私有函数在函数前加一个下划线\_
* 变量
  * 变量名尽量小写, 如有多个单词，用下划线隔开
  * 常量采用全大写，如有多个单词，使用下划线隔开

### 保留字

```
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```



