### 语法

```
compile(source, filename, mode[, flags[, dont_inherit]])
```

### 作用

将一个字符串编译为字节代码

### 参数

* source:字符串或者AST（Abstract Syntax Trees）对象。。

* filename:代码文件名称，如果不是从文件读取代码则传递一些可辨认的值。

* mode:指定编译代码的种类。可以指定为 exec, eval, single。
* flags:变量作用域，局部命名空间，如果被提供，可以是任何映射对象。。
* flags和dont\_inherit是用来控制编译源码时的标志

### 返回值

### 实例

```
>>>str = "for i in range(0,10): print(i)" 
>>> c = compile(str,'','exec')   # 编译为字节代码对象 
>>> c
<code object <module> at 0x10141e0b0, file "", line 1>
>>> exec(c)
0
1
2
3
4
5
6
7
8
9
>>> str = "3 * 4 + 5"
>>> a = compile(str,'','eval')
>>> eval(a)
17
```



