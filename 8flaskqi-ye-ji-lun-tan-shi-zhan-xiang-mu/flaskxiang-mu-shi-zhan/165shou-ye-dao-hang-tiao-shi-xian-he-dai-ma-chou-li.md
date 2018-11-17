### 1.相关链接

组件:

### 2.抽离模板

```
<meta name="csrf-token" content="{{ csrf_token() }}">
<script src="http://cdn.bootcss.com/jquery/3.1.1/jquery.min.js"></script>
<link href="http://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
<script src="{{ url_for('static',filename="common/zlajax.js") }}"></script>
<link rel="stylesheet" href="{{ url_for('static',filename="common/sweetalert/sweetalert.css") }}">
<script src="{{ url_for('static',filename="common/sweetalert/sweetalert.min.js") }}"></script>
<script src="{{ url_for('static',filename="common/sweetalert/zlalert.js") }}"></script>
```

### 3.导航条模板

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    {% include "common/_heads.html" %}
    <title>
        {% block title %}{% endblock %}
    </title>
    {% block head %}{% endblock %}
</head>
<body>
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                        data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <a class="navbar-brand" href="#">论坛</a>
            </div>

            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                    <li class="active"><a href="#">首页<span class="sr-only">(current)</span></a></li>
                </ul>
                <form class="navbar-form navbar-left">
                    <div class="form-group">
                        <input type="text" class="form-control" placeholder="请输入关键字">
                    </div>
                    <button type="submit" class="btn btn-default">搜索</button>
                </form>
                <ul class="nav navbar-nav navbar-right">
                    <li><a href="{{ url_for("front.signin") }}">登陆</a></li>
                    <li><a href="{{ url_for("front.signup") }}">注册</a></li>
                </ul>
            </div><!-- /.navbar-collapse -->
        </div><!-- /.container-fluid -->
    </nav>
    {% block  body %}

    {% endblock %}
</body>
</html>
```

### 4.首页

```
{% extends "front/base.html" %}

{% block title %}
    Tokimeki论坛
{% endblock %}


{% block head %}

{% endblock %}


{% block body %}
    {{ self.title() }}
{% endblock %}
```



