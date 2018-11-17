## 视图

* 在django中，视图对web请求进行回应
* 视图接受request对象作为第一个参数，包含了请求的信息
* 视图就是一个python函数，被定义在views.py中

```
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.

def index(request):
    return HttpResponse("index")

def detail(request,id):
    return HttpResponse("detail %s" % id)
```

* 定义完成视图后，需要配置urlconf，否则无法处理请求

---

## URLconf

* 在Django中，定义URLconf包括正则表达式、视图两部分
* Django使用正则表达式请求的URL，一旦匹配成功，则调用应用的视图
* 注意:只匹配路径部分，即除去域名、参数后的字符串
* 在test1/urls.py插入myapp，使主urlconf连接到myapp.urls模块

![](/assets/urlconf.png)

```
from django.conf.urls import url
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    url(r'^',include('myapp.urls')),
]
```

* 在myapp中的urls.py中添加urlconf

```
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^',views.index),
    url(r'^([0-9]+)/$',views.detail),
]
```



