# 104 Flask-Restful插件的基本使用

## 安装

```text
pip install flask-restful
```

## 定义Restful的视图

使用flask-restful，那么定义视图函数的时候，就要继承自flask\_restful.Resource类，然后再根据当前请求的method来定义相应的方法。比如期望客户端是使用get方法发送过来的请求，那么就定义一个get方法。类似于MethodView。

```text
from flask import Flask,render_template,url_for
from flask_restful import Api,Resource

app = Flask(__name__)
# 用Api来绑定app
api = Api(app)

# Json数据
class IndexView(Resource):
    def get(self,username=None):
        return {"username":"angle"}
# 可以指定多个url
api.add_resource(IndexView,'/index/<username>/','/regist/',endpoint='index')

with app.test_request_context():
    print(url_for('index',username='angle'))

if __name__ == '__main__':
    app.run(debug=True)
```

注意事项:

1. endpoint是用来给url\_for反转url的时候指定的。如果不写endpoint，那么将会使用视图的名字的小写作为endpoint。
2. add\_resource的第二个参数是访问这个视图函数的url，这个url可以跟之前的route一样，可以传递参数，并且还有一点不同的是，这个方法可以传递多个url来指定这个视图函数

