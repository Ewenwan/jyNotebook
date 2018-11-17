## CRSF

* 全称为Cross Site Request Forgery,跨站请求伪造
* 某些恶意网站上包含链接、表单按钮或者JavaScript，会利用登录过的用户在浏览器中的认证信息视图在web网站上完成默写操作，这就是跨站攻击
* 创建login用于展示表单
* 创建crsf用于接收post请求

```
def login(request):
    return render(request,'myapp/login.html')

def crsf(request):
    name = request.POST['name']
    context = {'name':name}
    return render(request,'myapp/crsf.html',context)
```

* 配置url

```
    url(r'^crsf/$',views.crsf),
    url(r'^login/$',views.login),
```

* 创建模板login.html用于展示表单

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form method="post" action="{% url 'myapp:crsf' %}">
        <input name="name"/><br />
        <input type="submit" value="提交" />
    </form>
</body>
</html>
```

* 创建模板crsf用于展示接收的结果

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {{ name }}
</body>
</html>
```

* 在访问中，如果报错如下:

![](/assets/crsf.png)

* 将settinsg.py的中间件代码"django.middleware.crsf.CrsfViewMiddleware"注释
* 查看login的源码，复制，在自己的网站内建一个HTML文件，粘贴源码，访问查看效果

---

### 访crsf的使用

* 在django的模板中，提供了防止跨站攻击的方法，使用步骤如下:
* 1.在settings.py中启动"django.middleware.crsf.CsrfViewMiddleware"中间件，此项在创建项目时，默认被启用
* 2.在login.html中添加标签

```
<form>
    {% csrf_token%}
    ....
</from>

```

* 3.测试刚才的两个请求，发现跨站的请求被拒绝了，效果如下:

![](/assets/crsf1.png)-

---

### 取消保护

* 如果某些视图不需要保护，可以使用装饰器crsf\_exempt，模板中也不需要写标签，修改crsf的视图

```
from django.views.decorators.csrf import  csrf_exempt

@csrf_exempt
def crsf(request):
    name = request.POST['name']
    context = {'name':name}
    return render(request,'myapp/crsf.html',context)
```

* 运行上面的两个请求，发现都可以请求

---

### 保护原理

加入标签后，可以查看源代码，发现多了如下代码

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form method="post" action="/crsf/">
        <input type='hidden' name='csrfmiddlewaretoken' value='T6CFH7Q5sIepoujVMrnFnpEtkErPQowirYBwDi2icLkJt9g3Eb9EC3TXQL0KDA7X' />
        <input name="name"/><br />
        <input type="submit" value="提交" />
    </form>
</body>
</html>
```

* 在浏览器的调试工具中，通过network标签可以查看cookie信息
* 本站中自动添加了cookie信息，如下图

![](/assets/csrf3.png)

* 查看跨站的信息，并没有cookie信息，即使加入上面的隐藏域代码，发现又可以访问了
* 结论：django的csrf不是完全的安全
* 当提交请求时，中间件'django.middleware.csrf.CsrfViewMiddleware'会对提交的cookie及隐藏域的内容进行验证，如果失败则返回403错误



