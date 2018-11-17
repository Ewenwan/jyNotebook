Python 编程中 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。

来看下while的语法

```
while 判断条件：
    执行语句……
```

执行语句可以是单个语句或语句块。判断条件可以是任何表达式，任何非零、或非空（null）的值均为true。

当判断条件假false时，循环结束。

实例:

```
>>> k = 1
>>> while k < 9:
...     print(k)
...     k+=1
...
1
2
3
4
5
6
7
8
```

可以使用continue，break 来跳过循环，continue 用于跳过该次循环，break 则是用于退出循环

```
i = 1
while i < 10:   
    i += 1
    if i%2 > 0:     # 非双数时跳过输出
        continue
    print(i)       # 输出双数2、4、6、8、10

i = 1
while 1:            # 循环条件为1必定成立
    print(i)         # 输出1~10
    i += 1
    if i > 10:     # 当i大于10时跳出循环
        break
```

### else语句

在 python 中，while … else 在循环条件为 false 时执行 else 语句块

```
>>> k = 1
>>> while k < 9:
...     print(k)
...     k+=1
... else:
...     print("循环结束了")
```

#### 简写语句

类似 if 语句的语法，如果 while 循环体中只有一条语句，可以将该语句与while写在同一行中

```
>>> while 1<2 : print("1小于2")
```

可以使用`Ctrl+C`来中断循环

