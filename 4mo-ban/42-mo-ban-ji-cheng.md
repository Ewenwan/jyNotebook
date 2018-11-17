## 模板继承

* 模板继承可以减少页面内容的重复定义，实现页面内容的重用
* 典型应用:网站的头部、尾部是一样的，这些内容可以定义在父模板中，子模板不需要重复定义
* block标签:在父模板中预留区域，在子模板中填充
* extends继承:继承，写在模板文件的第一行
* 定义父模板base.html

```
{%block block_name%}
这里可以定义默认值
如果不定义默认值，则表示空字符串
{%%endblock}
```

* 定义子模板main.html

```
{% extends "base.html" %}
```

* 在子模板中使用block填充预留区域

```
{% block block_name%}
实际填充内容
{%endblock%}
```

---

## 说明

* 如果在模板中使用extends标签，必须是模板中的第一个标签
* 不能在一个模板中定义多个相同名字的block标签
* 子模板不必定义全部父模板中的blocks，如果子模板没有定义block，则使用了父模板中的默认值
* 如果发现在模板中大量的赋值内容，那就应该把内容移动到父模板中
* 使用可以获取父模板中block的内容
* 为了更好的可读性，可以给endblock标签一个名字

```
{% block block_name%}
区域内容
{% endblock block_name%}
```

---

## 三层继承结构

* 三层阶乘结构使代码得到最大程度的复用，并且使得添加内容更加简单

* 常见的结构页面

![](/assets/电商页面.png)

---

### 创建根级目录

* 名称为"base.html"
* 存放整个站点共用的内容

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>
        {% block title %}
        {% endblock title %}
        商城
    </title>
</head>
<body>
    <div>
        top--{{ logo }}
        <hr />
        {% block left %}
        {% endblock %}
        {% block content %}
        {% endblock %}
        <hr />
        bottom
    </div>
</body>
</html>
```

### 创建分支模板

* 继承自base.html
* 创建base\_goods.html模板

```
{%  extends 'myapp/base.html' %}
{% block title %}
天使
{% endblock %}
{% block left %}
<h1>goods left</h1>
{% endblock %}
```

* 定义base\_user.html模板

```
{% extends 'myapp/base.html'%}
{% block title %}
用户中心
{% endblock %}
{% block left %}
    <h1 style="color:blue">user left</h1>
{% endblock %}
```

* 定义index.html，继承自base.html

```
{% extends 'myapp/base.html' %}
{% block content %}
    首页内容
{% endblock %}
```

### 为具体页面创建模板，继承自分支模板

* 定义商品列表页goodslist.html

```
{% extends 'myapp/base_user.html' %}
{% block content %}
    商品正文列表
{% endblock %}
```

* 定义用户密码userpwd.html

```
{% extends 'myapp/base_user.html' %}
{% block content %}
    用户密码修改
{% endblock %}
```

#### 视图调用具体页面，并传递模板中需要的数据

* 首页视图index

```
def index(request):
    return render(request,'myapp/index_two.html',{'logo':'首页'})
```

* 商品列表视图goodlist

```
def goodlist(request):
    return render(request,'myapp/goodslist.html',{'logo':'货物'})
```

* 用户密码视图userpwd

```
def userpwd(request):
    return render(request,'myapp/userpwd.html',{'logo':'密码'})
```

### 配置url

```
from django.conf.urls import url,include
from . import views

app_name = 'myapp'

urlpatterns = [

    url(r'^index/$',views.index_two),
    url(r'^list/$',views.goodlist),
    url(r'^pwd/$',views.userpwd),
]
```





