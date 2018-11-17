# 28 set和with语句以及模板中定义变量

在模板中，可以使用"set"语句来定义变量，示例如下:

```text
格式:
{% set 变量名=值 %}
{{ 变量名 }}
```

```text
"""html

<!--定义变量-->

{% set username="miku" %}
<p>用户名:{{ username }}</p>

"""
一旦定义了这个变量，那么后面的代码中，就可以使用这个变量


### 'with'语句:
'with'语句定义的变量，只能在'with'语句中使用，就不能再使用了，示例如下:
"""html
{% with classroom = "angle" %}
      <p>名字:{{ classroom }}</p>
{% endwith %}
{{ clssroom }}
"""

'with'语句也不一定要跟一个变量，可以定义一个空的'with'语句，以后在'with'块中通过'set'定义的变，就只能在这个'with'块中使用了:
"""html
{% with %}
    {% set classroom = "1班" %}
    <p>班级:{{classroom}}</p>
{% endwith %}
"""
```

```text
app.py

from flask import Flask, render_template

app = Flask(__name__)
app.config["TEMPLATES_ATUO_RELOAD"] = True

@app.route('/')
def hello_world():
    return render_template("index.html")


if __name__ == '__main__':
    # app.run(debug=True)
    app.run(host="0.0.0.0")
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
    <!--定义变量-->
    {% set username="angle" %}
    <p>用户名:{{ username }}</p>

    <div>
        {% with classroom="angle" %}
            <p>名字:{{ classroom }}</p>
        {% endwith %}
    {{ classroom }}
    </div>
</body>
</html>
```

