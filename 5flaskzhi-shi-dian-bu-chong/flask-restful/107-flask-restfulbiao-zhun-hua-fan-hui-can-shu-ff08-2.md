# 107 Flask-Restful标准化返回参数（2）

### 重命名属性

重命名属性字段

```text
# 更改content属性的命名
resource_fields = {
        'title':fields.String,
        '内容':fields.String(attribute='content'),
    }
------------------------------------------------------
{
    "title": "angle",
    "内容": "angle"
}
```

## 默认值

为指定字段设置默认值

```text
resource_fields = {
        'content':fields.String(default="angle"),
    }
```

## 复杂结构

使用fields.List可以使字段的值为列表，使用fields.Nested可以使字段的值为字典

```text
class ProfileView(Resource):
    resource_field = {
        'username':fields,String,
        'age':fields.Integer,
        'school':fields.String,
        'tags':fields.List(fields.String),
        'more':fields.Nested{{
            'signature':fields.String,
        }}
    }
```

### flask\_restful\_demo.py

```text
from flask import Flask
import config
from flask_restful import Api,Resource,fields,marshal_with
from exts import db
from models import User,Tag,Article

app = Flask(__name__)
app.config.from_object(config)
db.init_app(app)
api = Api(app)

# class Article(object):
#     def __init__(self,title):
#         self.title = title
#         # self.content = content
#
# article = Article(title='angle')
#
# class ArticleView(Resource):
#     # 可以渲染指定字段
#     resource_fields = {
#         'title':fields.String,
#         'content':fields.String(default="angle"),
#     }
#
#     # restful规范中要求，被定义的参数
#     # 即使这个参数没有值，也应该返回，返回一个None回去
#
#     @marshal_with(resource_fields)
#     def get(self):
#         # return {"title":"xxx",'content':'xxx'}
#         # 可以返回模型
#         return article
# api.add_resource(ArticleView,'/article/',endpoint='article')

class ArticleView(Resource):

    resource_fields = {
        # 更换字段名称
        '标题':fields.String(attribute='title'),
        'content':fields.String,
        # 设置默认值
        'age':fields.Integer(default=18),
        'author':fields.Nested({
            'username':fields.String,
            'email':fields.String,
        }),
        'tags':fields.List(fields.Nested({
            'id':fields.Integer,
            'name':fields.String,
        }))
    }
    @marshal_with(resource_fields)
    def get(self,article_id):
        article = Article.query.get(article_id)
        return article
api.add_resource(ArticleView,'/article/<article_id>',endpoint='article')

@app.route('/')
def hello_world():
    user = User(username="angle",email='xxx@qq.com')
    article = Article(title='miku',content='miku')
    article.author = user
    tag1 = Tag(name='C/C++')
    tag2 = Tag(name='Python')
    article.tags.append(tag1)
    article.tags.append(tag2)
    db.session.add(article)
    db.session.commit()
    print(user)
    return 'Hello World!'


if __name__ == '__main__':
    app.run(debug=True)
```

### models.py

```text
from exts import db

# 用户
# 文章
# 关系:1对多
# 标签:多对多

# 文章-标签-中间表
article_tag_table = db.Table(
    'article_tag',
     db.Column('article_id',db.Integer,db.ForeignKey('article.id'),primary_key=True),
     db.Column('tag_id',db.Integer,db.ForeignKey('tag.id'),primary_key=True)
)

class User(db.Model):
    __tablename__ = 'user'
    id = db.Column(db.Integer,primary_key=True)
    username = db.Column(db.String(50))
    email = db.Column(db.String(50))

class Article(db.Model):
    __tablename__ = 'article'
    id = db.Column(db.Integer,primary_key=True)
    title = db.Column(db.String(100))
    content = db.Column(db.Text)
    # 定义外键
    author_id = db.Column(db.Integer,db.ForeignKey('user.id'))
    # 关系 一对多
    author = db.relationship("User",backref='articles')
    # 多对多
    tags = db.relationship("Tag",secondary=article_tag_table,backref='tags')

class Tag(db.Model):
    __tablename__ = 'tag'
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(50))
```

### manage.py

```text
from flask_script import Manager
from flask_restful_demo2 import app
from flask_migrate import MigrateCommand,Migrate
from exts import db
import models

manager = Manager(app)

Migrate(app,db)
manager.add_command('db',MigrateCommand)

if __name__ == '__main__':
    manager.run()
```

### config.py

```text
DB_USERNAME = 'root'
DB_PASSWORD = '123456'
DB_HOST = '127.0.0.1'
DB_PORT = '3306'
DB_NAME = 'flask_restful_demo'

DB_URI = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8'.format(DB_USERNAME,DB_PASSWORD,DB_HOST,DB_PORT,DB_NAME)

SQLALCHEMY_DATABASE_URI = DB_URI

SQLALCHEMY_TRACK_MODIFICATIONS = False
```

### exts.py

```text
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()
```

