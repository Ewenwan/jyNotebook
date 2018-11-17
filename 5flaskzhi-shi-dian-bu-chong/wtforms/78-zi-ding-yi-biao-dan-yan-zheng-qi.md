# 78 自定义表单验证器

```text
class LoginForm(Form):
.....
    # 1234
    captcha = StringField(validators=[Length(4,4)])

    # 自定义验证器
    # valiedate_name
    def validate_captcha(self,field):
        # print(type(field))
        # 字段数据值
        # print(field.data)
        if field.data != "1234":
            raise ValidationError("验证码错误")
```

