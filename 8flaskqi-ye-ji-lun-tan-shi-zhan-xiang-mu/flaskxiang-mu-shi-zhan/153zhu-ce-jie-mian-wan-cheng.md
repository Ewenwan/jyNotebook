定义注册模块的类视图

```
class SignupView(views.MethodView):

    def get(self):
        return render_template('front/signup.html')

    def post(self):
        pass
bp.add_url_rule(rule='/signup/',view_func=SignupView.as_view('/signup/'))
```

定义注册页面

```
{% from "common/_macros.html" import static %}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>论坛注册</title>
    <script src="http://cdn.bootcss.com/jquery/3.1.1/jquery.min.js"></script>
    <link href="http://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="http://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
    <style>
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
    </style>
</head>
<body>
    <div class="outer-box">
        <div class="logo-box">
            <a href="/">
                <img src="{{ static("common/images/logo.png") }}"/>
            </a>
        </div>
        <h2 class="page-title">论坛账号登录</h2>

        <div class="sign-box">
            <div class="form-group">
                <div class="input-group">
                    <input type="text" name="telephone" class="form-control" placeholder="手机号码">
                    <span class="input-group-btn">
                        <button class="btn btn-default">
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
                <input type="password" name="password" class="form-control" placeholder="密码">
            </div>
            <div class="form-group">
                <input type="password" name="password2" class="form-control" placeholder="确认密码">
            </div>
            <div class="form-group">
                <div class="input-group">
                    <input type="text" name="graph_captcha" class="form-control" placeholder="图形验证码">
                    <span class="input-group-addon">
                        图形验证码
                    </span>
                </div>
            </div>
            <div class="form-group">
                <button class="btn btn-warning btn-block">
                    立即注册
                </button>
            </div>
        </div>

    </div>
</body>
</html>
```



