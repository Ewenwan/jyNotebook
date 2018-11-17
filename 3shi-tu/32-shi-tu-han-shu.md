## 定义视图

* 本质就是一个质数
* 视图的参数:
  * 一个HttpRequest实例
  * 通过正则表达式组获取的位置参数
  * 通过正则表达式组获得的关键字参数
* 在应用目录下默认有views.py文件，一般视图都定义在这个文件中
* 如果处理功能过多，可以将函数定义到不同的py文件中

```
配置路由urls.py文件

"""
url(r'^index/$',views.index,name="index"),
"""

views.py
"""
from django.http import HttpResponse

def index(request):
    return HttpResponse("helloworld")
"""
```

---

## 错误视图

* Django原生自带几个默认的视图用于处理HTTP错误

### 404\(page not found\)视图

* defaults.page\_not\_found\(request,template\_name="404.html"\)
* 默认的404视图将传递一个变量给模板:request\_path,是导致错误的URL
* 如果Django在检测URLconf中的每个正则表达式后没有找到匹配的内容也将调用404视图
* 如果在settings中DEBUG设置为True，name将永远不会调用404视图，而是显示URLconf并带有一些调试信息
* 在templates中创建404.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Not Found</title>
</head>
<body>
    Not Found
</body>
</html>
```

* 在settings.py中·修改调试

```
# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = False

ALLOWED_HOSTS = ["*",]
```

* 请求一个不存在的地址

```
localhost:8000/notfound/
```

### 500\(server error\)视图

* defaults.server\_error\(request,template\_name="500.html"\)
* 在视图代码中出现运行时错误
* 默认的500视图不会传递变量给500.html模板URLconf并带有一些调试信息

### 400\(bad request\)视图

* defaults.bad\_request\(request,template\_name="400.html"\)
* 错误来自客户端的操作
* 当用户进行的操作在安全方面可疑的时候，例如篡改会话cookie



