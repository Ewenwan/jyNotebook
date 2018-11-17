# 60 relationship方法中的cascade参数详解（1）

如果将数据库得到外键设置为RESTRICT，那么在ORM层面，删除了父表中的数据，那么从表中的数据将会NULL。如果不想要这种情况发生，那么应该将这个值的nullable=False。

在SQLAlchemy，只要将一个数据添加到session中，和它相关联的数据都可以一起存入到数据库中了。这些是怎么设置的呢?其实是通过relationship的时候 ，有一个关键字参数cascade可以设置这些属性:

1. save-update:默认选项。在添加一条数据的时候，会把其他和它相关联的数据都添加到数据库中。这种行为就是save-update属性影响的。
2. delete:表示当删除某一个模型中的数据的时候，是否也删除掉使用relationship和它关联的数据。
3. delete-orphan:表示当对一个ORM对象解除了父表中的关联对象的时候，自己便会被删除掉。当然如果表中的数据被删除，自己也会被删除。这个选项只能用在一对多上，不能用在多对多以及多对一上。并且还需要在子模型中的relationship中，增加一个single\_parent=True的参数。
4. merge:默认选项。当在使用session.merge，合并一个对象的时候，会将使用了relationship相关联的对象也进行merge操作
5. expunge:移除操作的时候，会将相关联的对象也进行移除。这个操作只是从session中移除，并不会真正的从数据库中删除。
6. all:是对save-update，merge，refresh-expire，expunge，delete几种的填写

```text
"relationship("模型类",backref="另外一个模型类的属性",cascade="save-update,delete")"

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
    author = relationship("User", backref=backref("articles",cascade="save-update,delete"),cascade="save-update,delete")

class Comment(Base):
    __tablename__ = "comment"
    id = Column(Integer,primary_key=True,autoincrement=True)
    content = Column(Text,nullable=False)
    uid = Column(Integer,ForeignKey('user.id'))

    author = relationship("User")

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

    user = session.query(User).first()
    session.delete(user)

    session.commit()

if __name__ == "__main__":
    # my_init_db()
    operation()
```

