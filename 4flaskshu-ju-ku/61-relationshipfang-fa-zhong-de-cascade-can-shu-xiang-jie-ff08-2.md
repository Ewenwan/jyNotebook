# 61 relationship方法中的cascade参数详解（2）

```text
续上...

from sqlalchemy import create_engine, Column, Integer, Text, String, DateTime, String, Float, func, and_, or_, \
    ForeignKey, Table
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker,relationship,backref

HOSTNAME = '127.0.0.1'
PORT = "3306"
USERNAME = "root"
PASSWORD = "123456"
DATABASE = "xt_flask"
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)

engine = create_engine(DB_URI)
Base = declarative_base(engine)
session = sessionmaker(engine)()

class User(Base):
    __tablename__ = 'user'
    id = Column(Integer,primary_key=True,autoincrement=True)
    username = Column(String(50),nullable=False)

    # articles = relationship("Article",cascade="save-update,delete")
    # comments = relationship('Comment',cascade="save-update,delete")

class Article(Base):
    __tablename__ = 'article'
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    uid = Column(Integer,ForeignKey("user.id"))

    # 不会执行添加操作 -- not add Article
    # author = relationship("User",backref="articles",cascade="")
    # 保存并更新数据
    # delete:级删除
    # author = relationship("User", backref="articles", cascade="save-update,delete")
    # author = relationship("User", backref="articles", cascade="delete")

    # author = relationship("User", cascade="save-update,delete")
    # single_parent=True,唯一的父表
    # cascade="all"，除了delete-orphan都包含了
    author = relationship("User", backref=backref("articles",cascade="save-update,delete,delete-orphan,merge,expunge"),cascade="save-update",single_parent=True)

class Comment(Base):
    __tablename__ = "comment"
    id = Column(Integer,primary_key=True,autoincrement=True)
    content = Column(Text,nullable=False)
    uid = Column(Integer,ForeignKey('user.id'))

    author = relationship("User",backref="comments")

def my_init_db():
    Base.metadata.drop_all()
    Base.metadata.create_all()

    user = User(username="angle")
    article = Article(title="miku")
    article.author = user

    comment = Comment(content="xxxx")
    comment.author = user
    session.add(comment)
    session.add(article)
    session.commit()

def operation():
    # article = session.query(Article).first()
    # session.delete(article)

    # user = session.query(User).first()
    # # session.delete(user)
    # user.articles = []

    # user = User(id=1,username="angle2")
    # article = Article(id=2,title="angle3")
    # user.articles.append(article)
    # # 合并，主键重复，替换值，不重复，添加进去
    # session.merge(user)
    # session.merge(article)
    # 移除操作,与session.add()操作相反

    user = User(username="angle2")
    article = Article(title="angle3")
    article.author = user
    session.add(user)
    session.add(article)
    # 只会从会话中删除数据，不会从数据库把数据删除
    session.expunge(user)
    session.commit()

"""
用户--文章
删除用户可以删除所有文章
删除一遍文章，不会删除用户
"""

if __name__ == "__main__":
    # my_init_db()
    operation()
```

