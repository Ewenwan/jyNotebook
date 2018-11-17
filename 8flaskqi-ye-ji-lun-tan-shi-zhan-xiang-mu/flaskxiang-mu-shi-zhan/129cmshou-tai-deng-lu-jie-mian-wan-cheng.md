### 1.相关链接

官方文档：[https://v3.bootcss.com/getting-started/](https://v3.bootcss.com/getting-started/)

模板:[https://v3.bootcss.com/examples/signin/](https://v3.bootcss.com/examples/signin/)

### 2.定义登录视图

在apps/cms/views.py中添加登录模块

```
from flask import Blueprint,views,render_template,url_for

# 创建蓝图
# subdomain:子域名，需要做映射
bp = Blueprint("cms",__name__,url_prefix='/cms')

@bp.route('/')
def index():
    return "cms index"

# 采用类视图,重写get|post方法

class LoginView(views.MethodView):

    def get(self):
        return render_template('cms/login.html')

    def post(self):
        pass
# 添加视图
bp.add_url_rule('/login/',view_func=LoginView.as_view('login'))
```



