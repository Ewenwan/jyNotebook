表单验证

```
class SignupForm(BaseForm):
    telephone = StringField(validators=[Regexp(r"1[345789]\d{9}",message="请输入正确格式的手机号码")])
    sms_captcha = StringField(validators=[Regexp(r"\w{4}",message="请输入正确格式的短信验证码")])
    username = StringField(validators=[Regexp(r".{2,20}",message="请输入正确格式的用户名")])
    password1 = StringField(validators=[Regexp(r"[0-9a-zA-Z]{6,20}",message="请输入正确格式的密码")])
    password2 = StringField(validators=[EqualTo("password1",message="两次输入的密码不一致")])
    graph_captcha = StringField(validators=[Regexp(r"\w{4}",message="请输入正确格式的图形验证码")])
    # print(password1,password2)
    # 短信验证码验证
    def validate_sms_captcha(self,field):
        sms_captcha = field.data
        telephone = self.telephone.data
        sms_captcha_mem = zlcache.get(telephone)
        if not sms_captcha_mem or sms_captcha_mem.lower() != sms_captcha.lower():
            raise ValidationError(message="短信验证码错误")
    # 图形验证码验证
    def validate_graph_captcha(self,field):
        graph_captcha = field.data
        graph_captcha_mem = zlcache.get(graph_captcha)
        if not graph_captcha_mem:
            raise ValidationError(message="图形验证码错误")
```

post请求

```
class SignupView(views.MethodView):

    def get(self):
        return render_template('front/signup.html')

    def post(self):
        form = SignupForm(request.form)
        if form.validate():
            telephone = form.telephone.data
            username = form.username.data
            password = form.password1.data
            user = FrontUser(telephone=telephone,username=username,password=password)
            db.session.add(user)
            db.session.commit()
            return restful.success()
        else:
            print(form.get_error())
            return restful.params_error(message=form.get_error())
bp.add_url_rule(rule='/signup/',view_func=SignupView.as_view('/signup/'))
```



