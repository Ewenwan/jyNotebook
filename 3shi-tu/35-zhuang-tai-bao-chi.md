## 状态保持

* http协议是无状态的:每次请求都是一次新的请求，不会记得之前的通信的状态
* 客户端与服务端的一次通信，就是一次会话
* 实现状态保持的方式，在客户端或服务器端存储于会话有关的数据
* 储存方式包括cookie、session、会话一般指session对象
* 使用cookie，所有数据存储在客户端，注意不要储存敏感信息
* 推荐使用session方式，所有数据存储在服务器端，在客户端cookie中存储session\_id
* 状态保持的目的是在一段时间内跟踪请求者的状态，可以实现跨页米娜访问当前请求者的数据
* 注意:不同的请求者之间不会共享这个数据，与请求者一一对应

---

## 启用session

* 使用django-admin startproject创建的项目默认启用
* 在settings.py文件中

* 在INSETALLED\_APPS列表中添加

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',

    # 添加
    'django.contrib.sessions',

    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
]

在MIDDLEWARE_CLASSES列表中添加

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    #添加
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    # 'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

* 禁用会话:删除上面的指定的两个值，禁用会话将节省一些性能消耗

---

### 使用session

* 启用会话后，每个HttpRequest对象将具有一个session，是一个类字典对象
* get\(key,default=None\):根据键获取会话的值
* clear\(\):清除所有会话
* flush\(\):删除当前的会话数据并删除会话Cookie
* del request.session\['memeber\_id'\]:删除会话

* 在views.py文件创建视图

```
from django.shortcuts import render,redirect
from django.urls import reverse

def index(request):
    name = request.session.get('name',default="游客")
    print(request.session.get('name'),'2')
    return render(request,"myapp/index.html",{'name':name})

def login(request):
    return render(request,'myapp/login.html')

def login_handle(request):
    request.session['name'] = request.POST['name']
    print(request.POST['name'])
    return redirect(reverse("myapp:index"))

def logout(request):
    request.session.flush()
    return redirect(reverse('myapp:index'))
```

* 配置url

```
    主url:
    from django.conf.urls import include,url

    url(r'',include('myapp.urls',namespace='myapp')),

    应用url:
    from django.conf.urls import url
    from . import views

    url(r'login/$', views.login, name='login'),
    url(r'login_handle/$', views.login_handle, name='login_handle'),
    url(r'logout/$', views.logout, name='logout')
```

* 创建模板index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>session会话</title>
</head>
<body>

<h1>Hello,{{ name }}</h1>
<hr/>
<a href="{% url 'myapp:login' %}">登录</a>
<a href="{% url 'myapp:logout' %}">登出</a>
</body>
</html>
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
    <form method="post" action="{% url 'myapp:login_handle' %}">
        姓名: <input type="text" name="name"/><br />
        <input type="submit" value="value"/>
    </form>
</body>
</html>
```

---

## 会话过期时间

* set\_expiry\(value\):设置会话的超时时间
* 如果没有指定，则两个星期后过期
* 如果value是一个整数，会话将在values秒没有活动后过期
* 如果value是一个imedelta对象，会话将在当前时间加上这个指定的日期/时间过期
* 如果value为0，name会话的cookie将在用户的浏览器关闭时过期
* 如果value为None，name会话永不过期
* 修改视图中login\_handle函数,查看效果

```
def login_handle(request):
    request.session['name'] = request.POST['name']
    print(request.POST['name'])
    # request.session.set_expiry(10)
    # request.session.set_expiry(timedelta(days=5))
    # request.session.set_expiry(0)
    # request.session.set_expiry(None)
    return redirect(reverse("myapp:index"))
```

---

## 存储session

* 使用存储会话的方式，可以使用settings.py的SESSION\_ENGINE项指定
* 基于数据库的会话:这是django默认的会话存储方式，需要添加django.contrib.session到的INSTALLED\_APPS设置中，运行manage.py migrate在数据库中安装会话表，可显示指定为

```
SESSION_ENGINE='django.contrib.sessions.backends.db'
```

* 基于缓存的会话:只存在本地内在中，如果丢失则不能找回，比数据库的方式读写更快

```
SESSION_ENGINE='django.contrib.sessions.backends.cache'
```

* 可以将缓存和数据库同时使用:优先从本地缓存中获取，如果没有则从数据中获取

```
SESSION_ENGINE = 'django.contrib.sessions.backends.cached_db'
```

---

## 使用Redis缓存session

* 安装 django-redis、django-redis-session

  * pip install django-redis
  * pip install django-redis-sessions

* 修改settings中的配置

```
# 缓存
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "default"
REDIS_TIMEOUT=7*24*60*60
CUBES_REDIS_TIMEOUT=60*60
NEVER_REDIS_TIMEOUT=365*24*60*60
```

* 测试缓存是否成功

```
输入交互命令:python manage.py shell

In [1]: from django.core.cache import cache #引入缓存模块

In [2]: cache.set('v', '555', 60*60)      #写入key为v，值为555的缓存，有效期30分钟
Out[2]: True

In [3]: cache.has_key('v') #判断key为v是否存在
Out[3]: True

In [4]: cache.get('v')     #获取key为v的缓存
Out[4]: '555'
```

* redis数据库更多详细:http://django-redis-chs.readthedocs.io/zh\_CN/latest/\#cache-backend



* 管理redis的命令

```
下载地址:https://github.com/MicrosoftArchive/redis/releases
启动:net start redis
停止:net stop redis
重启:net restart redis
使用客户端连接服务器:redis-cli
keys *:查看所有的连接
get name:获取指定键的值
del name:删除指定名称的键
```



