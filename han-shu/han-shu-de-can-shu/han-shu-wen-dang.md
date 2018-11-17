### 什么是函数文档？

在程序的时候，有时候为了使代码可读性更高，有时候会在程序旁边进行注释，可是这样影响python代码的美观，这时就可以使用函数文档。

举个例子

```
def money(dollar):
    """
    美元 --> 人民币
    汇率暂定为6.5
    :param dollar:
    :return: dollar * 6.5
    """
    return dollar * 6.5

m = money(10)

print(m)
```

运行结果

```
65.0
```

这样做还有个好处，这样可以不用打开源码慢慢去找文档注释，这时可以通过特殊属性

`__doc__获取(注意doc两边分别两条下划线)`

```
print(money.__doc__)
```

运行结果

```
    美元 --> 人民币
    汇率暂定为6.5
    :param dollar:
    :return: dollar * 6.5
```

在不确定函数的用法的时候，可以使用help\(\)函数来查看函数的文档

```
print(help(money))
```

运行结果

```
Help on function money in module __main__:

money(dollar)
    美元 --> 人民币
    汇率暂定为6.5
    :param dollar:
    :return: dollar * 6.5

None
```



