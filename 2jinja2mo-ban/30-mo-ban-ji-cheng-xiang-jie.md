# 30 模板继承详解

## 为什么需要继承模板:

模板继承可以把一些公用的代码单独抽取出来放到一个父模板中，以后子模板直接就可以使用了。这样可以重复性的代码，以后修改起来比较方便

## 模板继承语法:

使用"extends"语句，来指明继承的父模板，父模板的路径，也是相对于'templates'文件夹下的绝对路径。示例代码如下:

```text
{% extends "base.html" %}
```

## block语法

在父模板中，只能定义一些公共的代码。子模板可能要根据具体的需要实现不同的代码，这时候父模板就应该有能力提供一个借口，让父模板来实现，从而实现具体业务需求的功能。

在父模板中:

```text
{% block block的名字 %}
{% endblock %}
```

在子模板中

```text
{% block block的名字 %}
子模板的代码
{% endblock%}
```

## 调用父模板代码block中的代码

默认情况下，子模板如果实现了父模板定义的block，那么子模板block中的代码就会覆盖掉父模板的代码。如果想要在子模板中仍然保持父模板中的代码，那么可以使用""来实现。

```text
{% block body_block %}


<p style="background-color:red;">

这是父模板的代码

</p>

{% endblock %}


{% extends "base.html"%}
{% block body_block %}
{{super()}}

<p style="background:pink;">
我是子模板中的代码
</p>

{% endblock %}
```

## 调用另外一个block中的代码

如果想要在另外一个模板中使用其他模板中的代码。那么可以通过""就可以了。示例代码如下:

```text
{% block title %}
    miku
{% endblock %}

{% block body_block %}
{{super()}}
{{self.title()}}
<p style="background:pink;">我是子模版中的代码</p>
```

## 其他注意事项

1. 子模板中的代码，第一行，应该是"extends"
2. 子模板中，如果要实现自己的代码，应该放到block中。如果放到其他地方，则不会被渲染

```text
app.py

from flask import Flask, render_template

app = Flask(__name__)
app.config.update({
    "TEMPLATES_AUTO_RELOAD":True,
    "DENUG":True,
})

@app.route("/")
def hello_word():
    return render_template("index.html")

@app.route("/list/")
def my_list():
    return render_template("course_detail.html")

if __name__ == '__main__':
    # app.run(debug=True)
    app.run(host="0.0.0.0")
```

```text
base.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}{% endblock %}</title>
    <style>
        .nav ul{
            overflow: hidden;
        }
        .nav ul li{
            float: left;
            margin: 0 20px;
        }
    </style>
</head>
<body>
    <nav class="nav">
        <ul>
            <li>首页</li>
            <li>课程详情</li>
            <li>视频教程</li>
            <li>关于我们</li>
            <li>{{ username }}</li>
        </ul>
    </nav>
    {% block body_block %}
        <p style="background:red;">这是父模板的代码</p>
    {% endblock %}
    <footer>
        这是底部
    </footer>
</body>
</html>
```

```text
course_detail.html

{% extends 'base.html' %}

{% block body_block %}
    课程详情代码
{% endblock %}
```

```text
index.html

{% extends 'base.html' %}

{% block title %}
miku
{% endblock %}

{% block body_block %}
    {{ super() }}
    {{ self.title() }}
    <p style="background:pink;">我是子模板中的代码</p>
{% endblock %}
```

