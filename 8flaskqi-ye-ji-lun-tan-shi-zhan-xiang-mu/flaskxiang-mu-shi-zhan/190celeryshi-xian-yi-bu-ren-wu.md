### 1.相关链接

celery:[http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html)

### 2.关系

![](/assets/190-1.png)

### 3.安装&准备

* redis
* 安装celery

```
pip install celery
```

* 在Windows操作系统上，还需要安装另外一个东西,eventlet

```
pip install eventlet
```

redis:[http://docs.celeryproject.org/en/latest/getting-started/brokers/redis.html\#broker-redis](http://docs.celeryproject.org/en/latest/getting-started/brokers/redis.html#broker-redis)

安装

```
pip install -U "celery[redis]"
```

配置

```
app.conf.broker_url = 'redis://localhost:6379/0'
-------------------------------------------------
redis://:password@hostname:port/db_number
```

### 4.tasks任务

```
#celery
# pip install celery
# 在Windows操作系统上，还需要安装另外一个东西,eventlet
# pip install eventlet


# task，任务
# broker(中间人)，存储任务的队列(借助redis实现)
# worker:真正执行任务的工作者
# backend:用来存储任务执行后的结果

from celery import Celery
import time

# 中间人:redis
# 存储结果的位置:backend
# Celery("当前模块的名字",broker="redis://host:port/0",backend="redis://host:port/0",)
celery = Celery("tasks",broker="redis://118.24.128.18:6379/0",backend="redis://118.24.128.18:6379/0")

@celery.task
def send_mail():
    print("邮件开始发送")
    time.sleep(5000)
    print("邮件发送结束")
```

### 5.主程序

```
from tasks import send_mail

if __name__ == "__main__":
    send_mail.delay()

# -A:application
# celery -A tasks.celery worker -l info -P eventlet
```

在命令行中运行

```
celery -A tasks.app worker -loglevel=info
```

出现以下错误

```
ValueError: not enough values to unpack (expected 3, got 0)
```

解决

```
pip install eventlet
```

```
celery -A <mymodule> worker -l info -P eventlet
或者
celery -A <mymodule>--pool=eventlet worker --loglevel=info
```

```
celery -A tasks.celery worker -l info -P eventlet
-------------------------------------------------
celery -A tasks.celery --pool=eventlet worker --loglevel=info
```



