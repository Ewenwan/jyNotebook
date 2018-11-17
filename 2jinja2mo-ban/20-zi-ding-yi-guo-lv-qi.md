# 20 自定义过滤器

```text
### 自定义模板过滤器
过滤器本质上就是一个函数，如果在模板中调用这个过滤器，那么就会将这个变量的值作为第一个参数传给过滤器这个函数，然后函数的返回值会作为这个过滤器的返回值
使用到一个装饰器:@app.template_filter('my_cut')

# 指定一个名字
@app.template_filter('my_cut')
def cut(value):
    value = value.replace("hello",'')
    return value


<p>{{ article|my_cut }}</p>
"""
```

