### 什么是装饰器？

装饰器是一个很著名的设计模式，经常被用于有切面需求的场景，较为经典的有插入日志、性能测试、事务处理等。

### 装饰器有什么用？

抽离出大量函数中与函数功能本身无关的雷同代码并继续重用。概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能，也称之为扩展功能。

先看一个简单的例子:

```
def foo():
    print("this is a foo")

foo()
```

现在有一个新的需求，希望可以记录下函数的执行日志，于是在代码中添加日志代码

```
import logging


def foo():
    print("this is a foo")

    logging.warning("foo is running")


foo()
```

可是如果函数 bar\(\)、bar2\(\) 也有类似的需求，怎么做？再写一个 logging 在 bar 函数里？这样就造成大量雷同的代码，为了减少重复写代码，我们可以这样做，重新定义一个新的函数：专门处理日志 ，日志处理完之后再执行真正的业务代码

```
import logging


def use_logging(func):
    logging.warning("foo is running")
    func()

def foo():
    print("this is a foo")

use_logging(foo)
```

这样做逻辑上是没问题的，功能是实现了，但是调用的时候不再是调用真正的业务逻辑 foo 函数，而是换成了 use\_logging 函数，这就破坏了原有的代码结构， 现在不得不每次都要把原来的那个 foo 函数作为参数传递给 use\_logging 函数，那么有没有更好的方式的呢？当然有，答案就是装饰器。

### 简单装饰器

```
import logging


def use_logging(func):

    def wrapper():
        logging.warning("foo is running")
        # 注意，这把foo()函数当做参数传递进来了，执行func()相当于执行foo()
        return func()

    return wrapper


def foo():
    print("this is a foo")

# 因为装饰器use_logging(foo)返回的是函数对象wrapper，这条语句相当于 foo = wrapper
foo = use_logging(foo)
# foo = wrapper
# 执行foo()就相当于执行wrapper()
foo()
# wrapper()

# 上面的两句等价于下面的语句
# use_logging(foo)()
```

use\_logging 就是一个装饰器，它一个普通的函数，它把执行真正业务逻辑的函数 func 包裹在其中，看起来像 foo 被 use\_logging 装饰了一样，use\_logging 返回的也是一个函数，这个函数的名字叫 wrapper。在这个例子中，函数进入和退出时 ，被称为一个横切面，这种编程方式被称为面向切面的编程。

### @语法糖

@符号是装饰器的语法糖

##### 借鉴维基百科的看下什么是语法糖？

_语法糖（Syntactic sugar），也译为糖衣语法，是由英国计算机科学家彼得·蘭丁发明的一个术语，指计算机语言中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用。 语法糖让程序更加简洁，有更高的可读性_

```
import logging


def use_logging(func):

    def wrapper():
        logging.warning("foo is running")
        return func()

    return wrapper

@use_logging
def foo():
    print("this is a foo")


foo()
```

有了@，就可以省去foo = use\_logging\(foo\)这一句了，能够直接调用foo\(\)得到想要的答案，并且提高了程序的可重复利用性，并增加了程序的可读性

### 如何传参

传入一个参数

```
import logging


def use_logging(func):

    # 传入参数name
    def wrapper(name):
        logging.warning("{} is running".format(name))
        return func(name)

    return wrapper

@use_logging
def foo(name):
    print("this is a {}".format(name))


foo("foo")
```

传入多个参数

```
import logging


def use_logging(func):

    def wrapper(*args,**kwargs):
        logging.warning("{} is running".format(func.__name__))
        return func(*args,**kwargs)

    return wrapper

@use_logging
def foo(name,age,**params):
    print("name:{},age:{},sex:{}".format(name,age,params.get("sex")))


params = {
    "sex":"男"
}

foo("angle","18",**params)
```

### 带参数的装饰器

装饰器还有更大的灵活性，例如带参数的装饰器，在上面的装饰器调用中，该装饰器接收唯一的参数就是执行业务的函数 foo 。装饰器的语法允许在调用时，提供其它参数，比如`@decorator(a)`。这样，就为装饰器的编写和使用提供了更大的灵活性。比如，可以在装饰器中指定日志的等级，因为不同业务函数可能需要的日志级别是不一样的。

```
import logging


def use_logging(level):

    def decorator(func):

        def wrapper(*args,**kwargs):

            if level == "warning":
                logging.warning("{} is running".format(func.__name__))
            elif level == "info":
                logging.info("{} is running".format(func.__name__))

            return func(*args,**kwargs)

        return wrapper

    return decorator

@use_logging(level="info")
def foo(name,age,**params):
    print("name:{},age:{},sex:{}".format(name,age,params.get("sex")))


params = {
    "sex":"男"
}

foo("angle","18",**params)
```

上面的 use\_logging 是允许带参数的装饰器。它实际上是对原有装饰器的一个函数封装，并返回一个装饰器。我们可以将它理解为一个含有参数的闭包。当我 们使用`@use_logging(level="warn")`调用的时候，Python 能够发现这一层的封装，并把参数传递到装饰器的环境中。

`@use_logging(level="warn")`等价于`@decorator`

等价于如下

```
import logging


def use_logging(level):

    def decorator(func):

        def wrapper(*args,**kwargs):

            if level == "warning":
                logging.warning("{} is running".format(func.__name__))
            elif level == "info":
                logging.info("{} is running".format(func.__name__))

            return func(*args,**kwargs)

        return wrapper

    return decorator

def foo(name,age,**params):
    print("name:{},age:{},sex:{}".format(name,age,params.get("sex")))


params = {
    "sex":"男"
}

# 调用最外围函数
test = use_logging(level="warning")
# test = decorator
test(foo)("angle","18",**params)
```

### 类装饰器

没错，装饰器不仅可以是函数，还可以是类，相比函数装饰器，类装饰器具有灵活度大、高内聚、封装性等优点。使用类装饰器主要依靠类的\_\_call\_\_方法，当使用 @ 形式将装饰器附加到函数上时，就会调用此方法。

```
class Foo(object):
    def __init__(self, func):
        self._func = func

    def __call__(self):
        print ('class decorator runing')
        self._func()
        print ('class decorator ending')

@Foo
def bar():
    print ('bar')

bar()
```

### functools.wraps

使用装饰器极大地复用了代码，但是他有一个缺点就是原函数的元信息不见了，比如函数的docstring、\_\_name\_\_、参数列表，先看例子：

```
# 装饰器
def logged(func):
    def with_logging(*args, **kwargs):
        print func.__name__      # 输出 'with_logging'
        print func.__doc__       # 输出 None
        return func(*args, **kwargs)
    return with_logging

# 函数
@logged
def f(x):
   """does some math"""
   return x + x * x

logged(f)
```

不难发现，函数 f 被with\_logging取代了，当然它的docstring，\_\_name\_\_就是变成了with\_logging函数的信息了。好在我们有functools.wraps，wraps本身也是一个装饰器，它能把原函数的元信息拷贝到装饰器里面的 func 函数中，这使得装饰器里面的 func 函数也有和原函数 foo 一样的元信息了。

```
from functools import wraps
def logged(func):
    @wraps(func)
    def with_logging(*args, **kwargs):
        print func.__name__      # 输出 'f'
        print func.__doc__       # 输出 'does some math'
        return func(*args, **kwargs)
    return with_logging

@logged
def f(x):
   """does some math"""
   return x + x * x
```

### 装饰器顺序

假如一个函数同时有多个装饰器如下

```
def a(func):

    def wrapper(*args,**kwargs):
        print("a")
        return func(*args,**kwargs)

    return wrapper


def b(func):
    def wrapper(*args, **kwargs):
        print("b")
        return func(*args, **kwargs)

    return wrapper


def c(func):
    def wrapper(*args, **kwargs):
        print("c")
        return func(*args, **kwargs)

    return wrapper


def d(func):
    def wrapper(*args, **kwargs):
        print("d")
        return func(*args, **kwargs)

    return wrapper

@a
@b
@c
@d
def e1():
    print("e1")

def e2():
    print("e2")

e1()
print("-"*30)
a(b(c(d(e2))))()
```

运行结果

```
a
b
c
d
e1
------------------------------
a
b
c
d
e2
```

执行顺序是从里到外，最先调用最里层的装饰器，最后调用最外层的装饰器

