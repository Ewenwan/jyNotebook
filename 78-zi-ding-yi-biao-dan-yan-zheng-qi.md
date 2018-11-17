## 自定义表单验证器

1.定义一个方法，方法的语法格式:"validators\_字段名\(self,field\)"

```
class LoginForm(Form):
.....
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

2.在方法中，可以使用"field.data"获取字段的值

3.如果数据满足条件，那么可以什么都不做，可是如果失败了，那么应该抛出一个"wtforms.validators.Va;idationError"

