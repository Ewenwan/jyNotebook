## POST属性

* QueryDict类型的对象
* 包含post请求方式的所有参数
* 与form表单中的控件对应
* 表单中的那些控件会被提交
  * 控件要有name属性，则name属性的值为键，value属性的值为键，构成键值对提交
  * 对于CheckBox控，name属性一样为一组，当控件被选中后会被提交，存在一键多值的情况
* 值是可变的
* 定义视图login

```
def login(request):
    return render(request,'myapp/login.html')
```

* 配置路由url

```
    url(r'^login/$',views.login),
```

* 创建模板login.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form method="post" action="/main/">
        姓名: <input type="text" name="name"/><br />
        密码: <input type="password" name="pwd"/><br />
        性别: <input type="radio" name="sex" value="1" />男
              <input type="radio" name="sex" value="0"/>女<br />
        爱好: <input type="checkbox" name="hobby" value="c/c++"/>c/c++
              <input type="checkbox" name="hobby" value="python"/>python
              <input type="checkbox" name="hobby" value="java"/>java
              <input type="checkbox" name="hobby" value="C#"/>C#
        <input type="submit" value="value"/>
    </form>
</body>
</html>
```

* 创建视图main接收请求的数据

```
def main(request):
    name = request.POST['name']
    password = request.POST['pwd']
    sex = request.POST['sex']
    hobby = request.POST.getlist('hobby')
    context = {'name':name,'password':password,'sex':sex,'hobby':hobby}
    return render(request,'myapp/main.html',context)
```

* 配置路由urls.py

```
url(r'^main/$',views.main),
```

* 创建模板main.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {{ name }}
    {{ password }}
    {{ sex }}
    {{ hobby }}
</body>
</html>
```

* 注意:使用表单提交，注释掉settings.py中的中间件crsf

```
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    # 'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```



