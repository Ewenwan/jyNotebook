# 89 实战项目-中国工商银行注册功能完成

## ICBC.py

```text
from flask import Flask,render_template,views,request
from forms import RegistForm
from exts import db
import config
from models import User

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



if __name__ == '__main__':
    app.run(debug=True)
```

## config.py

```text
DB_URI = "mysql+pymysql://root:123456@localhost:3306/icbc?charset=utf8"

SQLALCHEMY_DATABASE_URI = DB_URI

SQLALCHEMY_TRACK_MODIFICATIONS = False
```

## models.py

```text
from exts import db

class User(db.Model):
    # 数据库表名
    __tablename__ = "user"
    # db.Column:字段
    id = db.Column(db.Integer,primary_key=True)
    email = db.Column(db.String(50),nullable=False)
    username = db.Column(db.String(50),nullable=False)
    password = db.Column(db.String(50),nullable=False)
    deposit = db.Column(db.Float(50),default=0)
```

## manage.py

```text
# 管理
from flask_script import Manager
from ICBC import app
from exts import db
# 迁移
# Migrate用来绑定app和db的
# MigrateCommand:迁移命令
from flask_migrate import MigrateCommand,Migrate
# 导入模型,便于执行迁移时，检测到模型
from models import User

# 创建一个实例化管理对象，具有app的功能
manager = Manager(app)

# 绑定
Migrate(app,db)
# 映射迁移命令:db
manager.add_command('db',MigrateCommand)
# 初始化仓库
# python manage.py db init
# 执行迁移
# python manage.py db migrate
# 把数据模型映射到数据库中
# python manage.py db upgrade


if __name__ == "__main__":
    manager.run()
```

## exts.py

```text
# 存储db

from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()
```

## forms.py

```text
# 字段类型
from wtforms import Form,StringField,FloatField
# 验证
from wtforms.validators import Email,Length,EqualTo,InputRequired

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
```

## regist.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>中国工商注册页面</title>
</head>
<body>
    <form action="" method="post">
        <table>
            <tbody>
                <tr>
                    <td>邮箱:</td>
                    <td><input type="emial" name="email"/></td>
                </tr>
                <tr>
                    <td>用户名:</td>
                    <td><input type="text" name="username"/></td>
                </tr>
                <tr>
                    <td>密码:</td>
                    <td><input type="password" name="password"/></td>
                </tr>
                <tr>
                    <td>重复密码:</td>
                    <td><input type="password" name="password_repeat"/></td>
                </tr>
                <tr>
                    <td>余额:</td>
                    <td><input type="text" name="deposit"/></td>
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

## index.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>中国工商银行首页</title>
</head>
<body>
    <h1>欢迎来到中国工商银行</h1>
    <div>
        <ul>
            <li><a href="{{ url_for("regist") }}" >立即注册</a></li>
        </ul>
    </div>
</body>
</html>
```

