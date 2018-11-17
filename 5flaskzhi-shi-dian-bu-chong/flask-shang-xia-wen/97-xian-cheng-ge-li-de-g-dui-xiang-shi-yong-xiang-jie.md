# 97 线程隔离的g对象使用详解

g对象是整个flask应用运行期间都是可以使用的，并且也是跟request一样的，是线程隔离的，这个对象是专门用来存储开发者自定定义的一些数据，方便在整个flask程序中都可以使用，一般使用就是，将一些经常会用到的数据绑定到上面，以后就直接从g上面去就可以了

```text
from flask import Flask,request,current_app,url_for,g
from werkzeug.local import Local,LocalStack
from utils import log_a,log_b,log_c

from threading import local

# 只要绑定在Local对象上的属性，在每个线程中都是隔离的
# Thread Local
# flask = werkzeug+sqlalchemy+jinja

# global --> g

app = Flask(__name__)

@app.route('/')
def index():
    # 获取当前app对象
    # print(current_app.name)
    print(url_for('my_list'))
    username = request.args.get("username")
    # log_a(username)
    # log_b(username)
    # log_c(username)
    g.username = username
    log_a()
    log_b()
    log_c()
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
```

```text
utils.py

from flask import g

def log_a():
    print("log a {}".format(g.username))

def log_b():
    print("log b {}".format(g.username))

def log_c():
    print("log c {}".format(g.username))
```

