# 37 add\_url\_rule和app.route原理剖析

## add\_url\_rule\(rule,endpoint=None,view\_func=None\)

这个方法用来添加url与视图函数的映射，如果没有填写，那么默认会使用"view\_func"的名字作为"endpoint"，以后再使用"url\_for"的时候，就要看在映射的时候有没有传递"endpoint"参数，如果传递了，那么就应该使用"endpoint"指定的字符串，如果没有传递，那么就应该使用"view\_func"的名字

## app.route\(rule,\*\*options\)装饰器

这个装饰器，其实也是使用"add\_url\_rule"来实现url与视图函数映射的

```text
app.py

from flask import Flask, url_for

app = Flask(__name__)

# endpoint='index' == > **options
@app.route('/',endpoint="index") # ==> decorator
# @decorator
def hello_world():
    # print(url_for("my_list"))
    print(url_for("miku"))
    return 'Hello World!'
# decorator(hello_world)

def my_list():
    return "列表页"

# view_func:视图函数
# rule:路由
# endpoint:可以配合url_for使用
# endpoint:为url去一个名字

# app.add_url_rule(rule="/list/",view_func=my_list)
app.add_url_rule(rule="/list/",endpoint="miku",view_func=my_list)

with app.test_request_context():
    print(url_for("index"))

if __name__ == '__main__':
    app.run(debug=True)
```

