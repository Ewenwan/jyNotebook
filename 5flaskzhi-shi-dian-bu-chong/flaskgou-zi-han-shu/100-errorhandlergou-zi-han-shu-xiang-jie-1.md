# 100 errorhandler钩子函数详解

errorhandler:errorhandler接收状态码，可以自定义返回这种状态码的响应的处理方法

```text
@app.route('/list/')
def my_list():
    session["user_id"] = 1
    # return 'my_list'
    # 将本页面设置为404页面
    # abort(404)
    user_id = request.args.get('user_id')
    if user_id == '1':
        return 'hello'
    else:
        abort(400)
    return render_template('index.html')

def serror_error(error):
    return "服务器刷新的太频繁"

@app.errorhandler(404)
def not_found(error):
    # return render_template("url"),状态码
    return render_template('404.html'),404

@app.errorhandler(400)
def param_error(error):
    return '参数不正确'
```

abort\(\)函数可以手动抛出相应的错误

