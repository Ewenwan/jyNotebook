## GET属性

* QueryDict类型的对象
* 包含get请求方式的所有参数
* 与url请求地址中的参数对应，位于？后面
* 参数的格式是键值对，如key1=value1
* 多个参数之间，使用&连接，如key1=value1&key2=value2
* 键是开发人员定下来的，值是可变的
* 示例如下：
* 创建视图getTest1用于定义链接 ，getTest2用于接收一键一值，getTest3用于接收一键多值                                                                                                            

```
def getTest1(request):
    return render(request,'myapp/getTest1.html')

def getTest2(request):
    a = request.GET['a']
    b = request.GET['b']
    context = {'a':a,'b':b}
    return render(request,'myapp/getTest2.html',context)

def getTest3(request):
    a = request.GET.getlist('a')
    b = request.GET.get('b')
    context = {'a':a,'b':b}
    return render(request,'myapp/getTest3.html',context)
```

* 配置路由urls.py

```
    url(r'^getTest1/$',views.getTest1),
    url(r'^getTest2/$',views.getTest2),
    url(r'^getTest3/$',views.getTest3),
```

* getTest1.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    链接1:一个键传递一个值
    <a href="/getTest2/?a=1&b=2">gettest2</a><br />
    <a href="/getTest3/?a=1&a=2&b=3">gettest3</a>
</body>
</html>
```

* getTest2.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    a:{{ a }} <br />
    b:{{ b }}
</body>
</html>
```

* getTest3.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    a:{% for item in a %}
        {{ item }}
        {% endfor %}
    <br />
    b:{{ b }}
</body>
</html>
```



