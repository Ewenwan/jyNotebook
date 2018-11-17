# 98 before\_request钩子函数详解

befor\_first\_request:处理第一次请求之前执行

```text
@app.before_first_request
def first_request():
    print("before_first_request")
```

before\_request:在每次请求之前执行。通常可以用这个装饰器来给视图函数增加一些变量

```text
@app.before_request
def before_request():
    # print("在视图函数执行之前执行的钩子函数")
    user_id = session.get("user_id")
    if user_id:
        g.user = 'angle'
```

