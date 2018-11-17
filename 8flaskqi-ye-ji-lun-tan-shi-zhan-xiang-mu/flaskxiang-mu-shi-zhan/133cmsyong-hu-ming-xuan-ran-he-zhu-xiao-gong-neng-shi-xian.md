使用g对象作为全局变量，便于获取用户

hooks.py

```
from .views import bp
import config
from flask import  session,g
from .models import CMSUser

# 钩子函数，在请求之前获取
@bp.before_request
def before_request():
    if config.CMS_USER_ID in session:
        user_id = session.get(config.CMS_USER_ID)
        user = CMSUser.query.get(user_id)
        if user:
            g.cms_user = user
```

为了代码不冗余，可以将代码提出来放在单独一个文件，但是这样就不会被运行，为了使用之运行，在\_\__init_\_.py中导入py

```
# from .hooks import before_request
import apps.cms.hooks
```



