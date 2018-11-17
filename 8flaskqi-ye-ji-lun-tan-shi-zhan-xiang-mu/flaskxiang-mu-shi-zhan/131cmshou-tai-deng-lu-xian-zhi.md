限制登录，防止没有登录账户，直接访问其他页面

```
from flask import session,redirect,url_for
from functools import wraps

def login_requeired(func):
    @wraps(func)
    def inner(*args,**kwargs):
        if 'user_id' in session:
           return func(*args,**kwargs)
        else:
            return redirect(url_for('cms.login'))
    return inner




@bp.route('/')
@login_requeired
def index():
    return "cms index"
```



