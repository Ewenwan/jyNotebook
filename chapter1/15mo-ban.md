## 模板

* 模板是HTML页面，可以根据视图中传递的数据填充值
* 创建模板的模板结构图

![](/assets/templates模板.png)

* 修改settings.py文件，设置TEMPLATES的DIR值

```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

* 在模板中访问视图传递的数据

```
{{输出值,可以是变量，也可以是对象.属性}}
{%执行代码%}
```

---

### 定义index.html模板

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
{{ number }}
    <h1>学生信息</h1>
    <ul>
        <li>
            <a href="{{student.pk}}">{{ student.pk }}--{{student.stu_name}}--{{ student.stu_date }}</a>
        </li>
    </ul>
</body>
</html>
```

```
views.py

"""
def index(request):
    student = students.objects.get(pk=1)
    # return HttpResponse(student.stu_date)
    return render(request,'myapp/index.html',{'student':student})
"""

注意要在urls.py添加路由
urlpatterns = [
    url(r'^index/$',views.index),
]

通过localhost:8000/index访问
```

---

### 定义detail.html模板

* 在模板中访问对象成员时，都以属性的方式访问，即方法也不能括号

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>详情页</title>
</head>
<body>
    <h1>{{ grade.gra_name }}班</h1>
    <ul>
        {% for student in grade.students_set.all %}

            <li>{{ student.stu_name }} ---- {{student.stu_sex }} --{{ student.stu_date }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

* 编译views.py文件，在方法中调用模板
* django提供了函数Render\(\)简化视图调用模板、构造上下文

```
from django.shortcuts import render
from django.http import HttpResponse
from django.template import RequestContext,loader
from .models import grades,students
# Create your views here.

# def index(request):
#     return HttpResponse("index")
#
# def detail(request,id):
#     return HttpResponse("detail %s" % id)

def index(request,id):
    student = students.objects.get(pk=id)
    # return HttpResponse(student.stu_date)
    return render(request,'myapp/index.html',{'student':student,'id':id})

def detail(request,id):
    grade = grades.objects.get(pk=id)
    return render(request,'myapp/detail.html',{'grade':grade})
```

---

```
urls.py文件配置路由

"""
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^index/(\d+)/$',views.index),
    url('detail/(\d+)/',views.detail),
]
"""
```

---

## 去除模板的硬编码

* 在index.html模板中，超链接是硬编码的，此时的请求地址为"127.0.0.1/index/1"

```
<a href="{{student.pk}}"}
```

* 如果建urlconf中详细页如下，链家就找不到了
* ```
  url('^grades/(\d+)/$',views.detail),
  ```
* 此时请求的地址为"localhost/grades/1"

* 问题:如果在模板中地址硬编码，将来urlconf修改后，地址将失效

* 解决:使用命名的url设置超链接

* 修改"text1/urls.py"文件,在include中设置namespace

```
from django.conf.urls import url
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    url(r'^',include(('myapp.urls',"myapp"),namespace="myapp")),
]
```

修改myapp/url.py文件，设置name

```
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^index/(\d+)/$',views.index,name="index"),
    url('bookdetail/(\d+)/',views.detail,name="detail"),
]
```

可以根据name来进行动态更改

---

#### render函数

将指定页面渲染后返回给浏览器

render\(request, template\_name\[, context\]）

结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的 HttpResponse 对象。

```
参数：
     request： 用于生成响应的请求对象。

     template_name：要使用的模板的完整名称，可选的参数

     context：添加到模板上下文的一个字典。默认是一个空字典。如果字典中的某个值是可调用的，视图将在渲染模板之前调用它。

     content_type：生成的文档要使用的MIME类型。默认为DEFAULT_CONTENT_TYPE 设置的值。

     status：响应的状态码。默认为200。
```



