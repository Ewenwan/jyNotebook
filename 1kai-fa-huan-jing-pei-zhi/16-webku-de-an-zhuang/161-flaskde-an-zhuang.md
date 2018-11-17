# 1.6.1 Flask的安装

## 1. 相关链接 {#1-相关链接}

* GitHub：[https://github.com/pallets/flask](https://github.com/pallets/flask)
* 官方文档：[http://flask.pocoo.org](http://flask.pocoo.org/)
* 中文文档：[http://docs.jinkan.org/docs/flask](http://docs.jinkan.org/docs/flask)
* PyPi：[https://pypi.python.org/pypi/Flask](https://pypi.python.org/pypi/Flask)
* 学习地址:[https://xintiaohuiyi.gitbook.io/flask-note/](https://xintiaohuiyi.gitbook.io/flask-note/)

## 2.安装

```text
pip install flask
```

## 3.验证安装

```text
from flask import Flask

# 创建一个Flask对象，传递__name__参数进去
# __name__参数的作用
# 1.可以规定规模和静态文件的查找路径
# 2以后一些flask插件，比如flask-migrate等，那么flask可以通过这个参数找到具体的错误
app = Flask(__name__)

# @app.route是一个装饰器
# @app.route('/')就是讲url中的/映射hello_world这个视图函数上面，那么flask可以通过这个参数找到
# hello_world这个函数，然后这个函数的返回值返回给浏览器

@app.route('/')
def hello_world():
    return 'hello world'

# 如果这个文件作为一个主文件运行，那么就执行app.run()方法
# 也就是启动这个网站
if __name__ == "__main__":
    # app.run()flask中的一个测试应用服务器
    # 如果设置参数host为0.0.0.0，外部机器也可以访问本机的网站
    # 没有设置，只能本机访问
    # app.run(host='0.0.0.0')
    app.run()
    # 改变端口
    # app.run(port=port)
```

运行代码后，可以在本机的5000端口开启web服务，控制台输出如下:

```text
* Serving Flask app "test_flask" (lazy loading)
* Environment: production
  WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
* Debug mode: off
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

直接访问 [http://127.0.0.1:5000/](http://127.0.0.1:5000/) ，可以看到网页上的内容:

![](../../.gitbook/assets/1.6.1-1.png)

