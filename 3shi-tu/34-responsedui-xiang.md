## HttpResponse对象

* 在django.http模块中定义了HttpResponse对象的API
* HttpRequest对象由Django自动创建，HttpResponse对象由程序员创建
* 不调用模板，直接返回数据

```
from django.http import HttpResponse

def index(request):
    return HttpResponse("你好")
```

* 调用模板

```
from djangp.http import HttpResponse

from django.template import RequestContext,loader

def index(request):
    templates = loader.get_template('myapp/index.html')
    context ={'h':'hello'}
    return HttpResponse(templates.render(context,request))
```

---

## 属性

* content:表示返回的内容，字符串类型
* charset:表示response采用的编码字符集，字符串类型
* status\_code:响应的HTTP响应状态码
* content-type:指定输出的MIME类型

## 方法

* init:使用也内容实例化HttpResponse对象
* write\(content\):以文件的方式写
* flush\(\):以文件的方式输出缓存区
* set\_cookie\(key,value=",max\_age=None,expires=None\):设置Cookie
  * key、value都是字符串类型
  * max\_age是一个整数目标是在指定秒数后过期
  * expires是一个datetime或timedelta对象，会话将在这个指定的日期/时间过期，注意datetime和timedelta值只有在使用PickleSerializer时才可序列化
  * max\_age与expires二选一
  * 如果不指定过期时间，则两个星期后过期

```
from django.http import HttpReponse
from datetime import *
```

* 创建cookie

```
from django.http import HttpResponse
def index(request):
    response = HttpResponse()
    cookie = request.COOKIES
    response.set_cookie('name', 'angle')
    #response.set_cookie('h1', '你好', None, datetime(2016, 10, 31))
    return response
```

* 在屏幕上输出cookie值

```
from django.http import HttpResponse
def index(request):
    response = HttpResponse()
    cookie = request.COOKIES
    response.write('<h1>' + cookie['name'] + '</h1>')
    return response
```

* delete\_cookie\(key\):删除指定的key的Cookie，如果key不存在则什么也不发生

---

## 子类HttpResponseRedirect

* 重定向，服务器端跳转
* 构造函数的第一个参数用来指定重定向的地址

```
from django.http import HttpResponse,HttpResponseRedirect
def index(request):
    return HttpResponseRedirect('js/')

def index2(request,id):
    return HttpResponse(id)
```

请求地址:127.0.0.1:8000/index

请求结果地址:127.0.0.1:8000/index/js/

* 反向解析

```
from django.urls import reverse

def index(request):
    print(reverse('myapp:index'))
    # /sunck/index/
    return render(request,'myapp/index.html')
```

* index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>学生信息</title>
</head>
<body>
    <h1>学生列表</h1>
    <a href="/good/123/">链接1</a> # {# 硬链接
    <a href="{% url 'myapp:good' 1%}">链接2</a> # {# 反向解析
</body>
</html>
```

* 请求地址:[http://localhost:8000/sunck/index/](http://localhost:8000/sunck/index/)
* 第一个链接:[http://localhost:8000/good/123/](http://localhost:8000/good/123/)
* 第二个链接:[http://localhost:8000/sunck/good/1](http://localhost:8000/sunck/good/1)

* 注意:

* 在urls.py中添加

  ```
  app_name = 'myapp'
  ```

* 在test2/urls.py中添加

```
url(r'^sunck/',include('myapp.urls',namespace='myapp')),
```

---

## 子类JsonResponse

* 返回json数据，一般用于异步请求
* _init_\(data\)
* 帮助用户创建json编码的响应
* 参数data是字典对象
* JsonResponse的默认Content-Type为application/json

```
from django.http import JsonResponse
def jsonTest(request):
    return JsonResponse({'list':'abc'})
    
配置路由:
url(r'^js/$',views.jsonTest,name="js"),
```

---

## 简写函数

### render

* render\(request,template\_name\[,context\]\)
* 结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的HttpResponse对象
* request:该request用于生产response
* template\_name:要使用的模板的完整名称
* context:添加到模板上下文的一个字典，视图将在渲染模板之间调用它

```
from django.shortcuts import render

def index(request):
    retuen render(request,'myapp/index.html',{'name':'angle'})
```

### **重定向**

* redirect\(url\)
* 为传递进来的参数返回HttpReponseRedirect
* url推荐使用反向解析

```
def showindex(request):
    print(reverse("myapp:index"))
    # return redirect(reverse('myapp:index'))
    return redirect('/sunck/index')
    return redirect(reverse('myapp:index'))
    
//重定向访问index.html
```

### 得到对象或返回404

* get_object_or-404\(klass,\*args,\*\*kwargs\)
* 通过模型管理器或查询集调用get\(\)方法，如果没有找到对象，不引发模型的DoesNotExist异常，而是引发Http404异常
* klass:获取对象的模型类、Manager对象或QuerySet对象
* \*\*kwargs:查询的参数，格式应该可以被get\(\)和filter\(\)接受
* 如果找到多个对象将引发MultipleObjectReturned

```
from django.shortcuts import  *

def detail(request,id):
    try:
        g = get_object_or_404(Grades,gname="python01")
    except Grades.MultipleObjectsReturned:
        return HttpResponse('error')
    return render(request,'myapp/detail.html',{'grade':g,"id":id})
    
# 将settings.py中的DEBUG改为False
# 将请求地址输入2和100查看效果
```

---

## 得列表或返回404

* get_list_or\_404\(klass,args,\*kwargs\)
* klass:获取列表的一个Model，Manager或QuerySet实例
* \*\*kwargs:查询的参数，格式应该可以被get\(\)和filter\(\)接受

```
from django.shortcuts import *

def index(request):
    list = get_list_or_404(Grades,pk__lt==6)
    return render(request,'myapp/detail.html',{'grade':g)
```

将settings.py中的DEBUG改为False

