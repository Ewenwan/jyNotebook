# 83 Flask设置和删除cookie\|Flask设置cookie过期时间\|设置Cookie的有效域名

* 设置cookie：设置cookie在Response对象上进行设置的，通过"flask.Response"对象上的一个"set\_cookie\(\)"方法来进行设置cookie信息

```text
# response对象
resp = Response("name")
# 设置cookie值
resp.set_cookie("name","value")
```

* 删除cookie：通过"flask.Response"对象上的一个"delete\_cookie\(\)"方法来进行设置cookie信息

```text
# 删除指定cookie
resp.delete_cookie("name")
```

* 设置cookie的有效期，默认有效期:知道浏览器关闭为止
  * 使用max\_age参数设置有效期事件
  * ```text
    # max_age:距离多少秒后cookie值过期
    resp.set_cookie("name","value",max_age=10)
    ```
  * 使用expires参数
  * ```text
    one:
    expires = datetime(year=2018,month=7,day=14,hour=16,minute=29,second=0)

    two:
    # 使用expires参数，就必须使用格林尼治时间
    # 要相对北京时间少8个小时
    expires = datetime(year=2018, month=7, day=14, hour=8, minute=29, second=0)

    three:
    # 设置距离多久
    expires = datetime.now() + timedelta(seconds=1) - timedelta(hours=8)

    resp.set_cookie("name", "value", expires=expires)
    ```
  * 注意:max\_age在IE8以下的浏览器是不支持的。expires在新班的http协议中被废弃，但是到目前为止所有的浏览器都能够支持它
  * ```text
    @app.route('/')
    def hello_world():
        # response对象
        resp = Response("name")
        # # 设置cookie值
        # max_age:距离多少秒后cookie值过期
        # resp.set_cookie("name","value",max_age=10)
        # expires = datetime(year=2018,month=7,day=14,hour=16,minute=29,second=0)
        # 使用expires参数，就必须使用格林尼治时间
        # 要相对北京时间少8个小时
        # expires = datetime(year=2018, month=7, day=14, hour=8, minute=29, second=0)
        # 设置距离多久
        # 在新版本的http协议中，expires参数视为废弃
        # 注意同时指定了expires参数和max_age参数，则使用max_age参数
        expires = datetime.now() + timedelta(seconds=1) - timedelta(hours=8)
        resp.set_cookie("name", "value", expires=expires)
        # 删除指定cookie
        # resp.delete_cookie("name")
        return resp
    # secure设置为True只能在HTTPS协议下使用
    # httponly设置为Truecookie只能被浏览器读取，不能被js读取
    # expires无效日期
    # max_age:以秒为单位，距离现在多久过期
    # set_cookie(self, key, value='',
    #            max_age=None, expires=None,
    #            path='/', domain=None,
    #            secure=False, httponly=False,
    #            samesite=None)
    ```
* 设置cookie的有效域名:cookie只能在主域名下使用。如果想要在子域名下使用，那么应该给"set\_cookie"传递一个"domain='.ty.com'"来指定其他子域名才能访问到这个cookie信息。

1.定义蓝图

```text
cmsviews.py
from flask import Blueprint
cms = Blueprint("cms",name,subdomain="cms")
@cms.route("/")
def index():
    return "cms 首页"
  cookie.demo.py

  ....
  from cmsviews import cms

  # 注册蓝图
  app.register_blueprint(cms)
  app.config["SERVER_NAME"] = "ty.com:5000"
  ....
```

2.地址映射:在hosts文件中添加以下映射

```text
127.0.0.1 ty.com
127.0.0.1 cms.ty.com
```

3.设置set\_cookie中的domain参数

```text
resp = Response("name")
resp.set_cookie("name", "value",domain=".ty.com")
```

