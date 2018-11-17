### 1.相关链接

官方文档:[https://pythonhosted.org/Flask-Mail/](https://pythonhosted.org/Flask-Mail/)

### 2.安装

```
pip install Flask-Mail
```

### 3.创建一个Mail对象

```
from flask_mail import Mail
...
mail = Mail(app)
```

惰性加载

```
from flask_mail import Mail

mail = Mail()
...
mail.init_app(app)
```

### 4.邮箱配置

```
# 邮箱配置MAIL_SERVER：默认'localhost'
# MAIL_PORT：默认25
# MAIL_USE_TLS：默认为False
# MAIL_USE_SSL：默认为False
# MAIL_DEBUG：默认app.debug
# MAIL_USERNAME：默认无
# MAIL_PASSWORD：默认无
# MAIL_DEFAULT_SENDER：默认无
# MAIL_MAX_EMAILS：默认无
# MAIL_SUPPRESS_SEND：默认app.testing
# MAIL_ASCII_ATTACHMENTS：默认为False
```

```
# MAIL_USE_TLS:端口号587
# MAIL_USE_SSL:端口号465
# QQ邮箱不支持非加密方式发送邮件
# 邮箱配置
# 发送者服务器地址
MAIL_SERVER = "smtp.qq.com"
MAIL_PORT = 587
MAIL_USERNAME = "154565621@qq.com"
# 授权码不是qq密码
MAIL_PASSWORD = "dasdaddasdasda"
MAIL_DEFAULT_SENDER = "154565621@qq.com"
MAIL_USE_TLS = True
```

### 5.发送邮件

```
from exts import db,mail
from flask_mail import Message

@bp.route('/email/')
def send_email():
    # subject:主题
    # recipients:接收者，列表类型，可以有多个接收者
    # body:发送的邮件的内容
    # sender:发送者，这个参数，可以修改发送者
    message = Message(subject='邮件发送',recipients=['154565621@qq.com'],body='测试')
    mail.send(message)
    return "发送成功"
```



