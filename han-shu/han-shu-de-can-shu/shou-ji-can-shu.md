### 什么是收集参数？

在定义函数的时候，不知道这个函数有多少个参数，因为在工作开发的时候，需要根据实际情况添加和删除参数的，这就造成了参数的不确定，由于添加和删除参数工作有点繁琐，所以这时才有了收集参数，收集参数是为了解决这个问题而出现的，收集参数两种，一种是将参数打包元组，一种是以字典形式打包

### \*args

先来讲下第一种，只需要在参数前面加上一个星号\(\*\)就可以了

```
def person(*args):
    print('{0}的年龄是{1},性别{2}'.format(args[0],args[1]))


person('angle',18)
```

运行结果

```
angle的年龄是18,性别未知
```

参数在传过去的时候，会进行打包成元组传递过去

如果想要单独额外指定参数，可以使用关键字参数

```
def person(*args,sex='未知'):
    print('{0}的年龄是{1},性别{2}'.format(args[0],args[1],sex))


person('angle','18',sex='男')
```

运行结果

```
angle的年龄是18,性别男
```

星号其实既可以打包又可以解包。什么是解包?

举个小栗子

将列表a传入test参数的收集参数\*args中

```
def test(*args):
    print("{} 个参数".format(len(args)))
    print("第二个参数:{}".format(args[1]))

a = [i for i in range(10)]
print(a)

test(a)
```

运行结果

```
Traceback (most recent call last):
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
1 个参数
  File "E:/JetBrains/Code_practice_project/test/fibonacci.py", line 8, in <module>
    test(a)
  File "E:/JetBrains/Code_practice_project/test/fibonacci.py", line 3, in test
    print("第二个参数:{}".format(args[1]))
IndexError: tuple index out of range
```

那么调用test\(a\)时便会出错，此时需要在a前面加上个星号\(\*\)表示实参需要解包后才能使用

```
def test(*args):
    print("{} 个参数".format(len(args)))
    print("第二个参数:{}".format(args[1]))

a = [i for i in range(10)]
print(a)

test(*a)
```

运行结果

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
10 个参数
第二个参数:1
```

### \*\*kwargs

另一种收集方式，用两个星号\(\*\*\)表示

```
def test(**kwargs):
  for key,value in kwargs.items():
      print("key:{},value:{}".format(key,value))


params = {
    "name":"angle","name":"angle",
    "age":18,
    "sex":"男",
}

test(**params)
```

运行结果

```
key:name,value:angle
key:age,value:18
key:sex,value:男
```

慢慢来解析一下是什么意思?

```
test(**params)这个是为了收集多个字典参数，打包传递过去
def test(**kwargs)是为了将字典进行解包，和前面讲过的是一样的
```



