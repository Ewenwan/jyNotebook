# 77 WTForms常用验证器

数据发过来时，经过表单验证，因此需要验证器来进行验证，以下对一些常用的内置验证器进行讲解:

* Email:验证上传的数据是否为邮箱

```text
# 验证邮箱
email = StringField(validators=[Email()])
```

* EqualTo:验证上传的数据是否和另外一个字段相等，常用的就是密码和确认密码两个字段是否相等

```text
# EqualTo指定与之保持相同值的字段
password_repeat = StringField(validators=[Length(min=6,max=10),EqualTo("password")])
```

* InputRequired:原始数据的需要验证。如果不是特殊情况，应该使用InputRequired。

```text
# 验证用户是否输入
username = StringField(validators=[input_required()])
```

* Length:长度限制，有min和max两个值进行限制

```text
username = StringField(validators=[Length(min=3,max=10,message="用户名长度必须在3到10位之间")])
```

* NumberRange:数字的区间，有min和max两个值限制，如果处在两个数字之间则满足

```text
# 验证范围
age = IntegerField(validators=[NumberRange(12,18)])
```

* Regexp:自定义正则表达式

```text
# 正则表达式
phone = StringField(validators=[Regexp(r'1[34578]\d{9}')])
```

* URL:必须要是URL的形式

```text
# url验证
home_page = StringField(validators=[URL()])
```

* UUID:验证UUID

```text
# uuid值验证
uuid = StringField(validators=[UUID()])
```

## forms.py

```text
from wtforms import Form,StringField,IntegerField
from wtforms.validators import Length,EqualTo,Email,Regexp,input_required,NumberRange,URL,UUID

# 继承Form
class RegistForm(Form):
    # message指定错误信息
    username = StringField(validators=[Length(min=3,max=10,message="用户名长度必须在3到10位之间")])
    password = StringField(validators=[Length(min=6,max=10)])
    # EqualTo指定与之保持相同值的字段
    password_repeat = StringField(validators=[Length(min=6,max=10),EqualTo("password")])

class LoginForm(Form):
    # # 验证邮箱
    # email = StringField(validators=[Email()])
    # # 验证用户是否输入
    # username = StringField(validators=[input_required()])
    # # 验证范围
    # age = IntegerField(validators=[NumberRange(12,18)])
    # # 正则表达式
    # phone = StringField(validators=[Regexp(r'1[34578]\d{9}')])
    # # url验证
    # home_page = StringField(validators=[URL()])
    # uuid值验证
    uuid = StringField(validators=[UUID()])
```

## login.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录表</title>
</head>
<body>
    <form action="" method="POST">
        <table>
            <tbody>
                <tr>
                    <td>邮箱:</td>
                    <td><input type="text" name="email"/></td>
                </tr>
                <tr>
                    <td>用户民:</td>
                    <td><input type="text" name="username"/></td>
                </tr>
                <tr>
                    <td>年龄:</td>
                    <td><input type="text" name="age"/></td>
                </tr>
                <tr>
                    <td>手机号:</td>
                    <td><input type="text" name="phone"/></td>
                </tr>
                <tr>
                    <td>个人主页:</td>
                    <td><input type="text" name="home_page"/></td>
                </tr>
                <tr>
                    <td>UUID:</td>
                    <td><input type="text" name="uuid"/></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" value="立即注册"/></td>
                </tr>
            </tbody>
        </table>
    </form>
</body>
</html>
```

myapp.py

```text
@app.route("/login/",methods=["GET","POST"])
def login():
    if request.method == "GET":
        return render_template("login.html")
    else:
        # 将表单数据传递给LoginForm进行验证
        form = LoginForm(request.form)
        if form.validate():
            return "successful"
        else:
            return "fail"

#uuid值:fab3e92a-13b0-4938-bae8-5e58066ae11d
# from uuid import uuid4
# print(uuid4())
```

