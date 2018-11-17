### 什么是递归？

递归就是不停的调用自己，也就是不停重复做某一个事情

举个小栗子

```
def f(n):
    if n <= 1:
        return 1
    return f(n-1)*n

n = int(input('请输入一个数字:'))
number = f(n)
print("阶乘结果:{}".format(number))
```

怎么来理解这个函数了

这里假设输入3

![](/assets/1.2.13.1.4-1.png)

运行结果

```
请输入一个数字:3
阶乘结果:6
```



