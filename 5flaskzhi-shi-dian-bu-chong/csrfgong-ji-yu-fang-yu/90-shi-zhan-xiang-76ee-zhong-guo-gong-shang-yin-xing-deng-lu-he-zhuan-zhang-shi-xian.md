# 90 实战项目-中国工商银行登录和转账实现

## ICDB.py

```text
from flask import Flask, render_template, views, request, session, redirect,url_for
from forms import RegistForm,LoginForm,TransferForm
from exts import db
import config
from models import User
from auth import login_required

app = Flask(__name__)
# 初始化app
db.init_app(app)
# 导入配置
app.config.from_object(config)

# 首页
@app.route('/')
def index():
    return render_template("index.html")

# 注册模块
class RegistView(views.MethodView):

    # get请求
    def get(self):
        return render_template("regist.html")
    # post请求
    def post(self):
        # request.form:获取所有表单数据
        # 将表单数据传入RegistForm中进行验证数据是否输入正确
        form = RegistForm(request.form)
        # 如果验证成功则会通过validate()方法返回一个True，反之False
        if form.validate():
            # 通过form.字段名.data获取表单数据
            email = form.email.data
            username = form.username.data
            password = form.password.data
            deposit = form.deposit.data
            # 创建user对象
            user = User(email=email,username=username,password=password,deposit=deposit)
            # 插入数据库中
            #-------------
            # 添加对象
            db.session.add(user)
            # 提交到数据库中
            db.session.commit()
            return "注册成功"
        else:
            # form.errors:验证失败错误的原因
            print(form.errors)
            return "注册失败"
# 通过类，进行添加url
app.add_url_rule("/regist/",view_func=RegistView.as_view("regist"))

# 登录
class LoginView(views.MethodView):

    def get(self):
        return render_template("login.html")

    def post(self):
        form = LoginForm(request.form)
        if form.validate():
            email = form.email.data
            password = form.password.data
            user = User.query.filter(User.email==email,User.password==password).first()
            if user:
                session["user_id"] = user.id
                # return "登录成功"
                return redirect(url_for("index"))
            else:
                return "邮箱或密码错误!"
        else:
            return render_template("login.html")
app.add_url_rule(rule="/login/",view_func=LoginView.as_view("login"))

# 转账
class TransferView(views.MethodView):

    decorators = [login_required]

    def get(self):
        return render_template("transfer.html")

    def post(self):
        form = TransferForm(request.form)
        if form.validate():
            email = form.email.data
            money = float(form.money.data)
            user = User.query.filter(User.email==email).first()
            print(user.deposit)
            if user:
                # 从会话中读取用户id
                user_id = session.get("user_id")
            #     # 如果没登录就跳转登录页面
            #     if user_id is None:
            #         return redirect(url_for("login"))
            #     print(user_id)
                # User.query.get()以id进行查询
                myself = User.query.get(user_id)
                print(type(myself.deposit))
                if myself.deposit >= money:
                    user.deposit += money
                    myself.deposit -= money
                    db.session.commit()
                    return "转账成功"
                else:
                    return "余额不足"
            else:
                return "该用户不存在"
        else:
            return "数据填写不正确"
app.add_url_rule(rule="/transfer/",view_func=TransferView.as_view("transfer"))

if __name__ == '__main__':
    app.run(debug=True)
```

## transfer.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>中国工商银行转账页面</title>
</head>
<body>
    <form action="" method="post">
        <table>
            <tbody>
                <tr>
                    <td>转到邮箱:</td>
                    <td><input type="text" name="email"/></td>
                </tr>
                <tr>
                    <td>转到金额:</td>
                    <td><input type="text" name="money"/></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" value="立即转账"/></td>
                </tr>
            </tbody>
        </table>
    </form>
</body>
</html>
```

## forms.py

```text
# 字段类型
from wtforms import Form,StringField,FloatField,IntegerField
# 验证
from wtforms.validators import Email,Length,EqualTo,InputRequired,NumberRange
# from models import User

class RegistForm(Form):
    # 验证是否是邮箱格式
    email = StringField(validators=[Email()])
    # 验证输入的长度是否达到3~20
    username = StringField(validators=[Length(3,20)])
    # 同上
    password = StringField(validators=[Length(6, 20)])
    # 验证是否和password字段的值一样
    password_repeat = StringField(validators=[EqualTo("password")])
    # 判断是否输入值
    deposit = FloatField(validators=[InputRequired()])

class LoginForm(Form):
    # 注意一定要Email填上括号
    email = StringField(validators=[Email()])
    password = StringField(validators=[Length(6,20)])

    # # 自定义验证器
    # def validate_password(self):
    #     pass

    # 验证等同于post请求里面的验证
    # def validate(self):
    #     # 调用父类
    #     result = super(LoginForm,self).validate()
    #     if not result:
    #         return False
    #     # 获取数据
    #     email = self.email.data
    #     password = self.password.data
    #     # 利用模型从数据库中过滤信息
    #     user = User.query.filter(User.email == email,User.password == password).first()
    #     if not user:
    #         self.email.errors.append("邮箱或密码错误")
    #         return False
    #     return True

class TransferForm(Form):
    email = StringField(validators=[Email()])
    money = FloatField(validators=[NumberRange(1,10000000)])
```

## login.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>中国工商银行登录界面</title>
</head>
<body>
    <form action="" method="post">
        <table>
            <tbody>
                <tr>
                    <td>邮箱:</td>
                    <td><input type="text" name="email"/></td>
                </tr>
                <tr>
                    <td>密码:</td>
                    <td><input type="password" name="password"/></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" valule="登录"/></td>
                </tr>
            </tbody>
        </table>
    </form>
</body>
</html>
```

## auth.py

```text
from functools import wraps
from flask import session
from flask import redirect,url_for

# 验证，防止跨越权限访问
def login_required(func):
    @wraps(func)
    def wrapper(*args,**kwargs):
        user_id = session.get("user_id")
        if user_id:
            return func(*args,**kwargs)
        else:
            return redirect(url_for("login"))
    return wrapper
```

