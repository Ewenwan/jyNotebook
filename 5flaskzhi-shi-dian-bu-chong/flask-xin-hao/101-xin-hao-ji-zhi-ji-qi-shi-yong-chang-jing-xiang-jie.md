# 101 信号机制及其使用场景详解

## 安装

```text
pip install blinker
```

## 自定义信号:自定义信号分三步，第一是定义一个信号，第二是监听一个信号，第三是发送一个信号。

* 定义信号:定义信号需要使用到blinker这个包的Namespace类来创建一个命名空间。比如定义一个在访问了某个视图函数的时候的信号。示例代码如下:

```text
from blinker import Namespace

# Namespace的作用:为了防止多人开发的时候，信号名字冲突的问题

mysignal = Namespace()
visit_signal = mysignal.signal('visit-signal')
```

* 监听信号:监听信号使用singel对象的connect方法，在这个方法中需要传递一个函数，用来接收以后监听到这个信号该做的事情。示例代码如下:

```text
def visit_func(sender,username):
    print(sender,username)
```

* 发送信号:发送信号使用singal对象的send方法，这个方法可以传递一些其他参数过去。示例代码如下:

```text
mysignal.send(username='angle')
```

### signal\_demo.py

```text
from flask import Flask,request,render_template
from blinker import Namespace
from signals import login_signal

# # Namespace 命名空间
# # 1.定义信号
# namespace = Namespace()
# fire_signal = namespace.signal('fire')
#
# # 2.监听信号
# def fire_test(sender):
#     print(sender)
#     print("start fire")
# fire_signal.connect(fire_test)
#
# # 3. 发送一个信号
# fire_signal.send()


# 定义一个登陆的信号，以后用户登录进来以后就发送一个登陆信号，然后能够监听这个信号,然后能够监听这个信号，在监听到这个信号以后，就记录当前这个用户登录的信息，用信号的方式，记录用户的登录信息

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

@app.route('/login/')
def login():
    username = request.args.get('username')
    if username:
        login_signal.send(username=username)
        return '登录成功'
    else:
        return '请输入用户名'

if __name__ == '__main__':
    app.run(debug=True)
```

### signals.py

```text
from blinker import Namespace
from datetime import datetime
from flask import request

namespace = Namespace()

login_signal = namespace.signal('login')

# 监听
def login_log(sender,username):
    # print('用户登录')
    # 记录 用户名，登录时间，ip地址
    username = username
    now = datetime.now()
    ip = request.remote_addr
    log = "登录日志:用户名:{},登录时间:{},ip地址:{}\n".format(username,now,ip)
    print(log)
    with open('login_log.txt','a+',encoding='utf-8') as f:
        f.write(log)

login_signal.connect(login_log)
```

