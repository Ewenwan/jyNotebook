# 04 flask程序详解

从flask这个包中导入flask这个类

flask这个类是项目的核心，以后很多操作都是基于这个类的对象

注册url，注册蓝图都是基于这个类的对象

```text
from flask import Flask

# 创建一个flask对象，传递__name__参数进去
# __name__参数的作用
# 1.可以规定规模和静态文件的查找路径
# 2.以后一些flask插件，比如Flask-migrate,Flask-SQLAlchemy如果报错，那么flask可以通过这个参数找到
# 具体的错误位置
app = Flask(__name__)

# @app.route 是一个装饰器
# @app.route('/')就是将url中的/映射hello_world这个视图函数上面，以后访问网站的/目录的时候，会执行
# hello_world这个函数，然后将这个函数的返回值返回给浏览器

@app.route('/')
def hello_world():
    return 'Hello World!'

# 如果这个文件作为一个主文件运行，那么就执行app.run()方法
# 也就是启动这个网站
if __name__ == '__main__':
# app.run() flask中的一个测试应用服务器
    app.run()
    # 改变启动端口
    # app.run(port=port)
```

