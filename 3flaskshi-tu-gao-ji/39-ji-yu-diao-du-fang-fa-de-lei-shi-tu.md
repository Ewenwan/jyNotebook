# 39 基于调度方法的类视图

1. 基于方法类视图，是根据请求的"method"来执行不同的方法的，如果童虎是发送的"get"请求，那么将会执行这个类的"get'方法，如果用户发送的是"post"请求，那么将会执行这个类的"post"方法，其他的method类似的，比如"delete","put"...
2. 这种方式，可以让代码更加简洁，所有和"get"请求相关的代码都放在"get"方法中，所有和"post"请求相关的代码都放在"post"方法中，就不需要跟之前的函数一样，通过"request.method == "GET""来判断执行

```text
class LoginView(views.MethodView):
    def get(self):
        return render_template('login.html')

    def post(self):
        username = request.form.get('name')
        password = request.form.get('password')
        if username == 'angle' and password == '123456':
            return '成功'
        else:
            return "失败"

app.add_url_rule(rule='/login/',view_func=LoginView.as_view('login'))
```

![](../.gitbook/assets/39.1.png)

```text
class LoginView(views.MethodView):

"""
    def __render(self,error=None):
        return render_template('login.html', error=error)

    # get请求执行这个代码
    def get(self):
        return self.__render()
"""

    # get请求执行这个代码
    def get(self,error=None):
        return render_template('login.html',error=error)

    # post请求执行这个代码
    def post(self):
        username = request.form.get('name')
        password = request.form.get('password')
        if username == 'angle' and password == '123456':
            return '成功'
        else:
            # return render_template('login.html',error='用户名/密码错误')
            return self.get(error='用户名/密码错误')

app.add_url_rule(rule='/login/',view_func=LoginView.as_view('login'))
```

![](../.gitbook/assets/39.3.png)

