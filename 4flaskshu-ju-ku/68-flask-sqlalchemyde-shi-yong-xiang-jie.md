# 68 Flask-SQLAlchemy的使用详解

## 安装

```text
pip install  flask-sqlalchemy
```

## 数据库连接

```text
1.定义数据库连接字符串DB_URI
2.将定义好的数据库连接字符串DB_URI放到配置文件中
app.config["SQLALCHEMY_DATABASE_URI"] = DB_URI
3.使用"flask_sqlalchemy.SQLAlchemy"类定义一个对象，并将"app"传入进去
db = SQLAlchemy(app)
```

## 创建ORM模型

```text
1.定义模型，不使用"delarative_base"来创建一个基类，而是使用"db.Model"来作为基类
2.在模型类中，'Column'、'String'、'Integer'以及'relationship'等，直接使用db.xxx调用
"db.Column()"
3.在定义模型的时候，可以不写"__tablename__"，那么"flask_sqlalchemy"会默认使用当前的模型的名字转换成小写作为表的名字，
并且如果这个模型的名字使用了多个单词并且使用了驼峰命名法，那么会在多个单词之间会使用下划线进行连接。
'''
# user_model
class UserModel(db.Model)
    ....
'''
```

## 将ORM模型映射到数据库

```text
1.db.drop_all()
2.db.create_all()
```

## 使用session

```text
以后session也不需要使用"sessionmaker"来创建了，直接使用"db.session"就可以了。操作这个session的时候就跟之前的"sqlalchemy"的
"session"是一样的。
```

## 查询数据

```text
如果查找数据只是查找一个模型上的数据，就可以通过"模型.query"的方式进行查找。"query"就跟之前的sqlalchemy中的query方法是一样的。
'''
user = User.query.filter(User.id == 1).all()
'''
```

## 完整代码

```text
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)

HOSTNAME = "127.0.0.1"
PORT = "3306"
DATABASE = "first_flask"
USERNAME = "root"
PASSWORD = "123456"
# dialect+dricer://username:password@host:port/database
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)

# 配置
app.config["SQLALCHEMY_DATABASE_URI"] = DB_URI
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False

# 数据库
# db == > app
# 通过db访问app
db = SQLAlchemy(app)

# 定义orm模型
# 继承自db.Model
# UserModel == > user_model
class User(db.Model):
    __tablename__ = "user"
    id = db.Column(db.Integer,primary_key=True,autoincrement=True)
    username = db.Column(db.String(50),nullable=False)

    def __repr__(self):
        return "<Article(username:%s)>" % self.username

class Article(db.Model):
    __tablename__ = "article"
    id = db.Column(db.Integer,primary_key=True,autoincrement=True)
    title = db.Column(db.String(50),nullable=False)
    uid = db.Column(db.Integer,db.ForeignKey("user.id"))

    author = db.relationship("User",backref=db.backref("articles"))

    def __repr__(self):
        return "<Article(title:%s)>" % self.title

@app.route('/')
def hello_world():
    return 'Hello World!'

def init_data():
    db.drop_all()
    db.create_all()
    user = User(username="angle")
    article = Article(title="title one")
    article.author = user
    # user.articles.append(article)
    db.session.add(article)
    db.session.commit()

def query():
    # db.session.query(User)与下面效果一样
    # order_by
    # filter
    # filter_by
    # group_by
    # join
    # subquery
    # user = User.query.filter(User.id == 1).all()
    # users = User.query.order_by(User.id.desc()).all()
    # print(users)
    # 过滤、删除
    user = User.query.filter(User.username == "angle3").first()
    db.session.delete(user)
    db.session.commit()

if __name__ == '__main__':
    # init_data()
    query()
    # app.run()
```

