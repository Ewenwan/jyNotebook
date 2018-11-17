# 76 WTForms表单验证基本使用

Flask-WTF是简化了WTForms操作的一个第三方库，WTForms表单的两个主要功能是验证用户提交数据的合法性以及渲染模板。当然还包括一些其他的功能:_CSRF保护_，文件上传等，安装Flask-WTF默认也会安装WTForms。

## 安装

```text
pip install flask-wtf
```

### 源码

### myapp.py

```text
from flask import Flask,request,render_template
from wtforms import Form,StringField
from wtforms.validators import Length,EqualTo

# 继承Form
class RegistForm(Form):
    # message指定错误信息
    username = StringField(validators=[Length(min=3,max=10,message="用户名长度必须在3到10位之间")])
    password = StringField(validators=[Length(min=6,max=10)])
    # EqualTo指定与之保持相同值的字段
    password_repeat = StringField(validators=[Length(min=6,max=10),EqualTo("password")])

app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'Hello World!'

@app.route("/regist/",methods=["GET","POST"])
def regist():
    if request.method == "GET":
        return render_template("regist.html")
    else:
        form = RegistForm(request.form)
        if form.validate():
            return "success"
        else:
            # 打印失败原因
            print(form.errors)
            return "fail"

if __name__ == '__main__':
    app.run(debug=True)
```

### regist.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>注册表</title>
</head>
<body>
    <form method="POST">
        <table>
            <tbody>
                <tr>
                    <td>用户名:</td>
                    <td><input type="text" name="username"/></td>
                </tr>
                <tr>
                    <td>密  码:</td>
                    <td><input type="text" name="password"/></td>
                </tr>
                 <tr>
                    <td>确认密码:</td>
                    <td><input type="text" name="password_repeat"/></td>
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

WTForms库有两个作用:第一个就是做表单验证，把用户提交上来的数据进行验证是否合法。第二个就是做模板渲染

## 表单验证

1.自定义一个表单类，继承自wtforms.Form类

```text
继承Form
class RegistForm(Form):
    # message指定错误信息
    username = StringField(validators=[Length(min=3,max=10,message="用户名长度必须在3到10位之间")])
    password = StringField(validators=[Length(min=6,max=10)])
    # EqualTo指定与之保持相同值的字段
    password_repeat = StringField(validators=[Length(min=6,max=10),EqualTo("password")])
```

2.定义需要验证的字段，字段的名字必须和模板中那些需要验证的input标签的那么属性值保持一致

3.在需要验证的字段上，需要指定好具体的数据类型

4.在相关的字段上，指定验证器

5.把表单数据\\(request.form\\)传递给RegistForm表单类，如果调用form.validate\\(\\)方法，如果返回True，那么代表用户输入的数据都是合法的，否则代表用户输入的数据是有问题的。如果验证失败了，那么可以通过form.error来获取具体的错误信息。

```text
# request.form:表单信息
form = RegistForm(request.form)
if form.validate():
   return "success"
else:
   # 打印失败原因
   print(form.errors)
   return "fail"
```

