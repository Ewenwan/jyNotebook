# 27 include标签使用详解

1. 这个标签相当于是直接指定的模板中代码复制粘贴到当前位置
2. "include"标签，如果想要使用父模板中的变量，直接使用就可以了，不需要使用“with context”
3. “include”的路径，也是跟"import"一样，直接从"templates"根目录下去找，不要以相对路径去找

```text
格式:
{% include "url" %}
```

```text
app.py


from flask import Flask, render_template

app = Flask(__name__)
app.config["TEMPLATES_AUTO_RELOAD"] = True

@app.route('/')
def hello_world():
    return render_template("index.html")

@app.route("/detail/")
def detail():
    return render_template("common/course_detail.html")

if __name__ == '__main__':
    app.run()
```

```text
index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>
        {% include "common/header.html" %}
            <div class="content">
                中简的
            </div>
        {% include "common/footer.html" %}
    </div>
</body>
</html>
```

```text
common/course_detail.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {% include "common/header.html" %}
    详情页
    {% include "common/footer.html" %}
</body>
</html>
```

```text
footer.html

<footer>
    这是底部的
</footer>
```

```text
header.html

<style type="text/css">
    .nav ul{
        overflow:hidden;
    }
    .nav ul li{
        float: left;
        margin: 0 20px;
    }
</style>

<nav class="nav">
    <ul>
        <li>首页</li>
        <li>课程详情</li>
        <li>视频教程</li>
        <li>关于我们</li>
    </ul>
</nav>
```

