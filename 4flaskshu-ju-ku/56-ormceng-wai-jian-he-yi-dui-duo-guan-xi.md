# 56 ORM层外键和一对多关系

mysql级别的外键，还不够ORM，必须拿到一个表中的外键，然后再去通过这个外键再去另外一张表查找

```text
# 表之间的关系
article = session.query(Article).first()
uid = article.uid
print(article)
# get方法只匹配主键字段
user = session.query(User).get(uid)
print(user)
print(uid)
```

可这样太麻烦了。SQLAlchemy提供了一个"relationship"，这个类可以定义属性，以后再访问相关联的表的时候就可以直接通过属性访问的方式就可以访问得到了。

```text
class User(Base):
    ....
    articles = relationship('Article')

    def __repr__(self):
        return "<User(username:%s)>" % self.username

class Article(Base):
    ....
    # 映射到User模型
    # backref:反向引用,为user添加一个属性
    author = relationship("User")

    def __repr__(self):
        return "<Article(title:%s),content:%s>" % (self.title,self.content)



article = session.query(Article).first()
print(article.author.username)

user = session.query(User).first()
print(user.articles)
```

另外，可以通过"backref"来指定反向访问的属性名称。articles是有多个，它们之间的关系是一对多

```text
class Article(Base):
    ......
    # 映射到User模型
    # backref:反向引用,为user添加一个属性
    author = relationship("User",backref="articles")
```

```text
from sqlalchemy import create_engine, Column, Integer, Text, String, DateTime, String, Float, func,and_,or_,ForeignKey
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker,relationship,backref
import random

HOSTNAME = '127.0.0.1'
PORT = "3306"
USERNAME = "root"
PASSWORD = "123456"
DATABASE = "xt_flask"
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)
from datetime import datetime

engine = create_engine(DB_URI)

Base = declarative_base(engine)

session = sessionmaker(engine)()

# 父表/从表
# user/article

class User(Base):
    __tablename__ = 'user'
    id = Column(Integer,primary_key=True,autoincrement=True)
    username = Column(String(50))

    # articles = relationship('Article')

    def __repr__(self):
        return "<User(username:%s)>" % self.username

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    content = Column(Text,nullable=False)
    uid = Column(Integer, ForeignKey("user.id", ondelete="SET NULL"))

    # 映射到User模型
    # backref:反向引用,为user添加一个属性
    author = relationship("User",backref="articles")

    def __repr__(self):
        return "<Article(title:%s),content:%s>" % (self.title,self.content)

# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user = User(username = 'angle')
# session.add(user)
# session.commit()
#
# article = Article(content='abc',title='123',uid=1)
# session.add(article)
# session.commit()

# # 表之间的关系
# article = session.query(Article).first()
# uid = article.uid
# print(article)
# # get方法只匹配主键字段
# user = session.query(User).get(uid)
# print(user)
# print(uid)

article = session.query(Article).first()
print(article.author.username)

user = session.query(User).first()
print(user.articles)
```

