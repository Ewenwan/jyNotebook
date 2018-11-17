# 29 加载静态文件

1. 加载静态文件使用的是"urf\_for"函数u，然后第一个参数需要为"static",第二个参数需要为"filename='路径' "，示例:

```text
{{ ur_for('static',filename="css/xxx.css") }}

格式:
{{ url_for('static',filename="在static下的相对路径") }}
```

```text
app.py

from flask import Flask, render_template

app = Flask(__name__)
app.config.update({
    'DEBUG':True,
    "TEMPLATES_AUTO_RELOAD":True,
})

@app.route('/')
def hello_world():
    return render_template("index.html")


if __name__ == '__main__':
    # app.run(debug=True)
    app.run(host="0.0.0.0")
```

```text
static/css/index.css


body{
    background-color:pink;
}
```

```text
static/js/index.js

alert("hello world")
```

```text
index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="{{ url_for('static',filename='css/index.css') }}">
    <script src="{{url_for('static', filename='js/index.js')}}"></script>
</head>
<body>
    <p></p>

</body>
</html>
```

