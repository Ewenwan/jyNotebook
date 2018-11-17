### 1.在生成验证码的时候存入memcached中

自定义memcached的set、get、delete操作，便于后期修改

```
import memcache

# debug=True，如果出现错误，会打印出来
cache = memcache.Client(["127.0.0.1:11211"],debug=True)

# 设置
def set(key,value,timeout=60):
    return cache.set(key,value,timeout)

# 获取
def get(key):
    return cache.get(key)

# 删除
def delete(key):
    return cache.delete(key)
```

将生成的验证码存入memcached中

```
zlcache.set(email,captcha)
```

### 2.利用ajax向服务器发起post请求

```
$(function () {
    $("#submit").click(function (event) {
        event.preventDefault();
        var emailE = $("input[name='email']");
        var captchaE = $("input[name='captcha']");

        var email = emailE.val();
        var captcha = captchaE.val();

        zlajax.post({
            'url': '/cms/resetemail/',
            'data': {
                'email': email,
                'captcha': captcha
            },
            'success': function (data) {
                if(data['code'] == 200){
                    console.log(captcha)
                    emailE.val("");
                    captchaE.val("");
                    zlalert.alertSuccessToast('邮箱修改成功！');
                }else{
                    zlalert.alertInfo(data['message']);
                }
            },
            'fail': function (error) {
                zlalert.alertNetworkError();
            }
        });
    });
});
```

### 3.接收post请求的表单数据，进行判断处理

```
class ResetEmailForm(BaseForm):
    email = StringField(validators=[Email(message='请输入正确格式的邮箱！')])
    captcha = StringField(validators=[Length(6,20)])

    def validate_captcha(self,field):
        print(field)
        captcha = field.data
        email = self.email.data
        captcha_cache = zlcache.get(email)
        print(captcha.lower(),captcha_cache.lower())
        if not captcha_cache or captcha.lower() != captcha_cache.lower():
            raise ValidationError('邮箱验证码错误！')

    def validate_email(self,field):
        email = field.data
        user = g.cms_user
        if user.email == email:
            raise ValidationError('不能修改为相同的邮箱！')
```

```
自定义验证器需要这样写

def validate_captcha(self.field):
    pass
```

### 4.处理验证过程

```
    def post(self):
        print(request.form)
        form = ResetEmailForm(request.form)
        if form.validate():
            email = form.email.data
            g.cms_user.email = email
            db.session.commit()
            return restful.success()
        else:
            return restful.params_error(form.get_error())
```



