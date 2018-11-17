## celery

* [官方网站](http://www.celeryproject.org/)
* [中文文档](http://docs.jinkan.org/docs/celery/)

* 示例一：用户发起request，并等待response返回。在本些views中，可能需要执行一段耗时的程序，那么用户就会等待很长时间，造成不好的用户体验

* 示例二：网站每小时需要同步一次天气预报信息，但是http是请求触发的，难道要一小时请求一次吗？

* 使用celery后，情况就不一样了

* 示例一的解决：将耗时的程序放到celery中执行

* 示例二的解决：使用celery定时执行

---

### 名词

* 任务task:就是一个python函数
* 队列queue:将需要执行的任务加入到队列中
* 人工worker:在一个新进程中，扶着执行队列中的任务
* 代理broker:负责调度，在布置环境中使用redis

### 使用

* 安装包

```
pip install celery
pip install django-celery
pip install celery-with-redis
```

* 配置settings.py

```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
    'tinymce',
    'haystack',
    'djcelery',
]
```

```
# celery
import djcelery
djcelery.setup_loader() # 初始化队列
BROKER_URL = 'redis://localhost:6379/0'
# 有密码
# BROKER_URL = 'redis://:123456@127.0.0.1:6379/0'
CELERY_IMPORTS = ('myapp.task')
# CELERY_IMPORTS = ('应用名称.task')
```

* 在应用目录下创建task.py文件

```
import time
from celery import task,shared_task

# 模拟一个耗时操作
@task
def timeTestOne():
    print("test1")
    time.sleep(10)
    print("test2")

@shared_task
def longtimeTest(n):
    time.sleep(n)
```

* 迁移，生成celery需要的数据表

```
python manage.py migrate
```

* 启动Redis

```
net start redis
```

* 启动worker

```
python manage.py celery worker --loglevel=info
```

* 调用语法

```
function.delay(parameters)
```

* 代码

```
import time
from .task import *
def celeryOne(request):
    print("angle")
    # time.sleep(3)
    longtimeTest.delay(1000)
    print("angle")
    return HttpResponse("成功")
```

* 使用delay\(\*arg,\*\*kwarg\)方法执行耗时的方法或者操作，并能传递参数值



