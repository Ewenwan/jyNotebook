抽离共同元素

```
{% from "common/_macros.html" import static %}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <title>{% block title %}{% endblock %}</title>
    <script src="http://cdn.bootcss.com/jquery/3.1.1/jquery.min.js"></script>
    <link href="http://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="http://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
    <script src="http://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
    <script src="{{ static('common/zlparam.js') }}"></script>
     <script src="{{ static("common/zlajax.js") }}"></script>
     <link rel="stylesheet" href="{{ static("common/sweetalert/sweetalert.css") }}">
    <script src="{{ static("common/sweetalert/sweetalert.min.js") }}"></script>
    <script src="{{ static("common/sweetalert/zlalert.js") }}"></script>
    {% block head %}

    {% endblock %}
</head>
<body>
    <div class="outer-box">
        <div class="logo-box">
            <a href="/">
                <img src="{{ static("common/images/logo.png") }}"/>
            </a>
        </div>
        <h2 class="page-title">
            {% block h2_block %}{% endblock %}
        </h2>

        <div class="sign-box">
            {% block signbox %}

            {% endblock %}
        </div>
    </div>
</body>
</html>
```

注册页面

```
{% extends 'front/signbase.html' %}
{% from "common/_macros.html" import static %}

{% block title %}
    论坛注册
{% endblock %}

{% block head %}
    <script src="{{ static("front/js/signup.js") }}"></script>
    <link href="{{ static("front/css/signup.css") }}" rel="stylesheet">
{% endblock %}

{% block h2_block %}
    论坛账号登录
{% endblock %}

{% block signbox %}
    <div class="form-group">
                <div class="input-group">
                    <input type="text" name="telephone" class="form-control" placeholder="手机号码">
                    <span class="input-group-btn">
                        <button  id="sms-captcha-btn" class="btn btn-default">
                            发送验证码
                        </button>
                    </span>
                </div>
            </div>
            <div class="form-group">
                <input type="text" name="sms_captcha" class="form-control" placeholder="短信验证码">
            </div>
            <div class="form-group">
                <input type="text" name="username" class="form-control" placeholder="用户名">
            </div>
            <div class="form-group">
                <input type="password" name="password1" class="form-control" placeholder="密码">
            </div>
            <div class="form-group">
                <input type="password" name="password2" class="form-control" placeholder="确认密码">
            </div>
            <div class="form-group">
                <div class="input-group">
                    <input type="text" name="graph_captcha" class="form-control" placeholder="图形验证码">
                    <span class="input-group-addon captcha-addon">
                <img id="captcha-img" class="captcha-img" src="{{ url_for('common.graph_captcha') }}" alt="">
                    </span>
                </div>
            </div>
            <div class="form-group">
                <span style="display: none;" id="return-to-span">{{ return_to }}</span>
                <button id="submit-btn" class="btn btn-warning btn-block">
                    立即注册
                </button>
            </div>
{% endblock %}
```

登录页面

```
{% extends 'front/signbase.html' %}
{% from "common/_macros.html" import static %}

{% block title %}
    论坛账号登录
{% endblock %}

{% block head %}
    <style>
        .reset-link{
            float: right;
        }
    </style>
{% endblock %}

{% block h2_block %}
    论坛账号登录
{% endblock %}

{% block signbox %}
    <div class="form-group">
        <input type="text" name="telephone" class="form-control">
    </div>
    <div class="form-group">
        <input type="password" name="password" class="form-control" placeholder="密码">
    </div>
    <div class="checkbox">
        <label>
            <input type="checkbox" name="remember" value="1"/>记住我
        </label>
    </div>
    <div class="form-group">
        <button id="submit-btn" class="btn btn-warning btn-block">
            立即登录
        </button>
    </div>
    <div class="form-group">
        <a href="{{ url_for("front.signup") }}" class="signup-link">没有账号?立即注册</a>
        <a href="#" class="reset-link">忘记密码?</a>
    </div>
{% endblock %}
```

渲染登录页面模板

```
class SigninView(views.MethodView):
    def get(self):
        return render_template("front/signin.html")

    def post(self):
        pass

bp.add_url_rule(rule='/signin/',view_func=SigninView.as_view('signin'))
```

共用css样式表

```
        body{
            background: #f3f3f3;
        }
        div[class=outer-box]{
            width:854px;
            background: #fff;
            margin: 0 auto;
            overflow: hidden;
        }
        .logo-box{
            text-align: center;
            padding-top:40px;
        }

        div > div[class=logo-box]  img{
            width:60px;
            height: 60px;
        }

        .page-title{
            text-align: center;
            font-family: 楷体;
        }

        .sign-box{
            width:300px;
            margin:0 auto;
            margin-top:50px;
        }

        .captcha-addon{
            padding:0;
            /*溢出隐藏*/
            overflow: hidden;
        }

        .captcha-img{
            width:94px;
            height:32px;
            cursor:pointer;
        }
```



