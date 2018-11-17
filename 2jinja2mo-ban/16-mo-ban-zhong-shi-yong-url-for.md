# 16 模板中使用url\_for

```text
url_for 笔记

模板中的'url_for'跟后台视图函数中的'urf_for'使用起来基本一模一样的，
也是传递视图函数的名字，也可以传递参数，需要在'url_for'左右两边加上一个{{}}
```

```text
from flask import Flask, render_template, url_for

app = Flask(__name__)

@app.route("/")
def hello_world():
    return render_template("index.html")

@app.route('/acounts/login/<id>/')
def login(id):
    # print(id)
    return render_template('login.html')

if __name__ == '__main__':
    app.run(debug=True)
```

```text
inde.html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
\{#    <a href="/acounts/login/">登录</a>#\}
\{#  \{\{ 用来存放变量 \}\}#\}
\{# \{% 用来执行函数或者逻辑代码 %\} #\}
<p><a href="{{ url_for('login',ref='/',id=1)}}">登录</a></p>
</body>
</html>
```

```text
login.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
登录页面
</body>
</html>
```



