### 1.相关链接

flask-celery:[http://flask.pocoo.org/docs/0.12/patterns/celery/](http://flask.pocoo.org/docs/0.12/patterns/celery/)

### 2.配置

```
from celery import Celery
from flask import Flask
from flask_mail import Message
from exts import mail
import config
from utils.sms import demo_sms_send

app = Flask(__name__)
app.config.from_object(config)
mail.init_app(app)

def make_celery(app):
    celery = Celery(app.import_name,backend=app.config["CELERY_RESULT_BACKEND"],broker=app.config["CELERY_BROKER_URL"])
    celery.conf.update(app.config)
    TaskBase = celery.Task
    class ContextTask(TaskBase):
        abstract = True
        def __call__(self, *args, **kwargs):
            with app.app_context():
                return TaskBase.__call__(self,*args,**kwargs)
    celery.Task = ContextTask
    return celery

celery = make_celery(app)

@celery.task
def send_mail(subject,recipients,body):
    message = Message(subject=subject,recipients=recipients,body=body)
    mail.send(message)

@celery.task
def send_sms_captcha(telephone,captcha):
    demo_sms_send.send_api(telephone, code=captcha)
```

```
# flask-celery配置
CELERY_BROKER_URL = "redis://118.24.128.18:6379"
CELERY_RESULT_BACKEND = "redis://118.24.128.18:6379"
```

### 3.发送邮件

```
@bp.route('/email_captcha/')
@login_required
def email_captcha():
    # /email_captcha/?email_capthca=xxx@qq.com
    email = request.args.get('email')
    if not email:
        return restful.params_error("请传递邮箱参数")
    # string.ascii_letters:返回a~z和A~Z的所有字母
    # 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    source = list(string.ascii_letters)
    source.extend(map(lambda x:str(x),range(10)))
    # 随机抽取6为数
    captcha = random.sample(source,6)
    captcha = "".join([k for k in captcha])

    # 给邮箱发送邮件
    # message = Message(subject="python论坛邮箱验证码",recipients=[email],body=captcha)
    # try:
    #     mail.send(message)
    # except:
    #     return restful.params_error()
    # key:email
    # value:captch
    send_mail.delay(subject="python论坛邮箱验证码",recipients=[email],body=captcha)
    zlcache.set(email,captcha)
    return restful.success()
```

### 4.发送短信验证码

```
@bp.route('/sms_captcha/',methods=['POST'])
def sms_captcha():
    # telephone
    # timestamp
    # md5(ts+telephone+salt)
    form = SMSCaptchaForm(request.form)
    if form.validate():
        telephone = form.telephone.data
        captcha = Captcha.gene_text(4)
        print("发送的短信验证码是:",captcha)
        send_sms_captcha(telephone=telephone,captcha=captcha)
        return restful.success()
        # if demo_sms_send.send_api(telephone,code=captcha):
        #     # 利用memcached进行缓存
        #     zlcache.set(telephone,captcha)
        #     return restful.success()
        # else:
        #     return restful.params_error(message="短信验证码发送失败！")
    else:
        return restful.params_error(message="参数错误")
```

### 5.启动

```
linux:
celery -A tasks.celery worker --pool=eventlet --loglevel=info
或者
windows:
celery -A tasks.celery worker --pool=solo--loglevel=info
```



