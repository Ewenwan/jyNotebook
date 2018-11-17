# 12-13 视图函数Response返回值详解

## 关于响应

视图函数的返回值会被自动转换一个响应对象，flask的转换逻辑如下:

* 如果返回的是一个合法的响应对象，则直接返回
* 如果返回的是一个字符串，那么flask会重新创建一个werkzeug.wrappers.Response对象，Response将给字符串作为主体，状态码是200，MIME类型为text/html,然后返回该Response对象
* 如果返回的是一个元组，元组中的数据类型是\(response.status.headers\)。status值会覆盖默认的200状态码，headers可以是一个列表或者字典，作为额外的消息头
* 如果以上条件都不满足，Flask会假设返回值是一个合法的wsgi应用程序

### 自定义响应

自定义响应必须满足三个条件:

* 必须继承自Response类
* 必须实现类方法force\_type\(cls,rv,environ=None\)
* 必须制定app.response\_clss为自定义的Response

## Reponse

### 视图函数中可以返回那些值

1. 可以返回字符串:返回的字符串其实是底层将这个字符串包装成了一个'Response'对象
2. 可以返回元组:元组的形式是\(响应体，状态码，头部信息，返回的元组在底层包装成了一个'Response'对象\)
3. 可以返回'Reponse'及其子类

### 实现一个自定义的Reponse对象:

1. 继承'Response'类
2. 实现方法'force\_type\(cls,rv,envison=None\)'
3. 指定'app.response\_class'为自定义的'Response'对象
4. 如果视图返回的数据，不是字符串，也不是元组，也不是Response，那么就会将返回值传给'force\_type',然后'force\_type'的返回值返回给前端

```text
from flask import Flask, Response, jsonify

# from werkzeug.wrappers import Response
# flask = werkzeug + sqlalchemy + jinja2

app = Flask(__name__)

# 将视图函数中返回的字典，转换成json对象，然后返回
class JSONResponse(Response):

    @classmethod
    def force_type(cls, response, environ=None):
        """
        这个方法只有视图函数返回非字符，非元组，非Response对象才会调用
        :param response:
        :param environ:
        :return:
        response，视图函数的返回值
        """
        print(response)
        if isinstance(response,dict):
            # 转换
            response = jsonify(response)
        return super(JSONResponse,cls).force_type(response,environ)

# 添加response类，一定要添加
app.response_class = JSONResponse

@app.route('/')
def hello_world():
    # return 'Hello World!'
    return Response('Hello World',status=200,mimetype='text/html')

# 设置cookie
@app.route('/list1/')
def list1():
    # return {"username":"miku"}
    # return ['a','b']
    # 以上数据不接回调，会报错
    resp = Response("list1")
    resp.set_cookie("miku","angle")
    return resp

# 添加响应头
@app.route('/list2/')
def list2():
    return "list2",200,{"X-NAME":"MIKU","Server":"windows2003"}

# json，非字符，非元组
@app.route('/list3/')
def list3():
    return {"username":"miku","age":16}

if __name__ == '__main__':
    app.run(debug=True)
```

