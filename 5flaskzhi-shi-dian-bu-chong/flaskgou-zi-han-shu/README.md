# Flask钩子函数

钩子函数:在代码中插入自己想要执行的代码

## 常用的钩子函数

befor\_first\_request:处理第一次请求之前执行

before\_request:在每次请求之前执行。通常可以用这个装饰器来给视图函数增加一些变量

teardown\_appcontext:不管是否有异常，注册的函数都会在每次请求之后执行

```text
@app.teardown_appcontext
def teardown(exc=None):
    if exc is None:
        db.session.commit()
    else:
        db.session.rollback()
    db.session.remove()
```

template\_filter:在jinja2模板的时候自定义过滤器，比如可以增加一个upper的过滤器

```text
### 自定义模板过滤器
过滤器本质上就是一个函数，如果在模板中调用这个过滤器，那么就会将这个变量的值作为第一个参数传给过滤器这个函数，然后函数的返回值会作为这个过滤器的返回值
使用到一个装饰器:@app.template_filter('my_cut')

# 指定一个名字
@app.template_filter('my_cut')
def cut(value):
    value = value.replace("hello",'')
    return value
```

context\_processor:上下处理器。返回的字典中的键可以在模板上下文中使用

errorhandler:errorhandler接收状态码，可以自定义返回这种状态码的响应的处理方法

