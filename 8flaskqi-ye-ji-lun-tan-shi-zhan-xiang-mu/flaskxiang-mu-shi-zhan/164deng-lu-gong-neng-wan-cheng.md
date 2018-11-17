登录signin类视图

```
class SigninView(views.MethodView):

    def get(self):
        return_to = request.referrer
        if return_to and return_to != request.url and return_to != url_for("front.signup") and safeutils.is_safe_url(return_to):
             return render_template("front/signin.html",return_to=return_to)
        else:
             return render_template('front/signin.html')

    def post(self):
        form = SigninForm(request.form)
        if form.validate():
            telephone = form.telephone.data
            password = form.password.data
            remember = form.remeber.data
            # 检索是否拥有这个账号
            user = FrontUser.query.filter_by(telephone=telephone).first()
            if user and user.check_password(password):
                session[config.FRONT_USER_ID] = user.id
                if remember:
                    session.permanent = True
                return restful.success()
            else:
                return restful.params_error(message="手机号码或者密码错误")
        else:
            return restful.params_error(message=form.get_error())
```

ajax传递表单数据

```
$(function () {
    $('#submit-btn').click(function (event) {
        event.preventDefault();
        var telephone_input = $("input[name='telephone']");
        var password_input = $("input[name='password']");
        var remember_input = $("input[name='remember']")

        var telephone = telephone_input.val();
        var password = password_input.val();
        var remember = remember_input.checked?1:0

        zlajax.post({
            'url':'/signin/',
            'data':{
                'telephone':telephone,
                'password':password,
                'remember':remember,
            },
            'success':function (data) {
                if (data['code'] == 200){
                    var return_to = $("#return-to-span").text();
                    if(return_to){
                        window.location = return_to;
                    }else{
                        window.location = '/';
                    }
                }
            },
            'fail':function () {

            },
        });
    });
});
```

登录表单验证

```
class SigninForm(BaseForm):
    telephone = StringField(validators=[Regexp(r"1[345789]\d{9}",message="请输入正确格式的手机号码")])
    password = StringField(validators=[Regexp(r"[0-9a-zA-Z]{6,20}",message="请输入正确格式的密码")])
    remeber = StringField()
```

设置配置文件config.py，定义前端用户会话名称

```
FRONT_USER_ID = 'FRONT_USER_ID'
```



