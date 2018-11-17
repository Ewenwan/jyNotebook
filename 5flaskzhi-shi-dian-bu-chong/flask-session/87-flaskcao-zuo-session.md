# 87 Flask操作session

* 设置session：设置session在session对象上进行设置的，通过"flask.session"对象上的一个"session.setdefault\(\)"方法或者字典来进行设置session信息

```text
# one
session.setdefault("name","angle")
# two
session["name"] = "angle"
```

* 获取session:通过"session.get\(\)"方法获取

```text
name = session.get("name")
```

* 删除指定session:通过“session.pop\(\)”方法删除指定的session值

```text
# 删除指定session
session.pop("name")
```

* 清除所有的session值

```text
# 清除所有session
session.clear()
```

* 设置session有效期:通过配置config进行这是，默认有效期为31天

```text
from datetime import timedelta
# 设置会话有效期时间:两个小时以后会话有效期时间过期
app.config['PERMANENT_SESSION_LIFETIME'] = timedelta(hours=2)

# 设置session的过期时间,permanent:持久性，默认时间为一个月
session.permanent = True
```

* 注意，使用session需要配置SECRET\_KEY

```text
import os
...
# os.unrandom(n):产生24位的随机数
app.config["SECRET_KEY"] = os.urandom(24)
```

