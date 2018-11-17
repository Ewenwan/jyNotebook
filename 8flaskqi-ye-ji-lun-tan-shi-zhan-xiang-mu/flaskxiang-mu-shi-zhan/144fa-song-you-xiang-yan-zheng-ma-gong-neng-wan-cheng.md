resetemail.html模板

```
{% extends 'cms/base.html' %}
{% from "common/_macros.html" import static %}

{% block title -%}
    修改邮箱
{%- endblock %}

{% block head %}
    <style>
        .form-container{
            width:300px;
        }
    </style>
    <script src="{{ static("cms/js/resetemail.js") }}"></script>
{% endblock %}

{% block page_title %}
    {{ self.title() }}
{% endblock %}

{% block main_content %}
    <form action="" method="post">
        <div class="form-container">
            <div class="form-group">
                <div class="input-group">
                    <input type="email" class="form-control" name="email" placeholder="新邮箱">
                    <span class="input-group-addon" id="captcha-btn" style="cursor: pointer">获取验证码</span>
                </div>
            </div>
            <div class="form-group">
                <input type="text" class="form-control" placeholder="邮箱验证码">
            </div>
            <div class="form-group">
                <button class="btn btn-primary">立即修改</button>
            </div>
        </div>
    </form>
{% endblock %}
```

resetemail.js

获取输入框内的值，然后利用Ajax异步发送

```
$(function () {
    $("#captcha-btn").click(function (event) {
        event.preventDefault();
        var email = $("input[name='email']").val()
        if(!email){
            zlalert.alertInfoToast("请输入邮箱");
            return;
        }
        zlajax.get({
            'url':"/cms/email_captcha/",
            "data":{
                'email':email,
            },
            'success':function (data){
                if (data["code"] == 200){
                    zlalert.alertSuccessToast("发送成功，请注意查收");
                }
                else{
                    zlalert.alertInfo(data["message"]);
                }
            },
            'fail':function(error){
                zlalert.alertNetworkError();
            }
        })
    })
});
```

发送验证码真正实现代码

```
@bp.route('/email_captcha/')
def email_captcha():
    # /email_captcha/?email_capthca=xxx@qq.com
    email = request.args.get('email')
    if not email:
        return restful.params_error("请传递邮箱参数")
    # string.ascii_letters:返回a~z和A~Z的所有字母
    # 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    source = list(string.ascii_letters)
    source.extend(map(lambda x:str(x),range(10)))
    # 随机抽取6为数
    captcha = random.sample(source,6)
    captcha = "".join([k for k in captcha])

    # 给邮箱发送邮件
    message = Message(subject="python论坛邮箱验证码",recipients=['1479852727@qq.com'],body=captcha)
    try:
        mail.send(message)
    except:
        return restful.params_error()
    return restful.success()
```



