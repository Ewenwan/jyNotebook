# 62 三种排序方式详解

1. order\_by:可以指定根据这个表中的某个字段进行排序，如果在前面添加了一个。，代表的是降序排序
   1. ```text
      默认正序排序
      降序排序
      articles = session.query(Article).order_by(Article.create_time.desc()).all()
      降序，在字段前面加个符号代表降序
      articles = session.query(Article).order_by("-create_time").all()
      articles = session.query(Article).all()
         for article in articles:
             print(article)
      ```
2. 在模型定义的时候指定默认排序:有些时候，不想每次在查询的时候都指定排序的方式，可以在定义模型的时候就指定排序的方式。有以下两种方式:  
   1. relationship的order\_by参数:在指定relationship的时候，传递order\_by参数来指定排序的字段  
   2. 在模型定义中，添加以下代码:  
   `__mapper_args__ = {    
   'order_by':title,    
   }`

   即可让文章用标题来进行排序

   1. ```text
      class Article(Base):
          __tablename__ = 'article'
          id = Column(Integer,primary_key=True,autoincrement=True)
          title = Column(String(50),nullable=False)
          # 注意default里面的datetime.now，没有()
          create_time = Column(DateTime,nullable=False,default=datetime.now)
          uid = Column(Integer,ForeignKey('user.id'))

          # author = relationship("User",backref=backref("articles",order_by=create_time.desc()))
          author = relationship("User", backref=backref("articles"))

          # 排序
          __mapper_args__ = {
              "order_by":create_time.desc(),
          }
      ```

3. 正向排序和反向排序:默认情况是从小到大，从前后排序的，可以调用排序的字段的desc方法
   1. ```text
      默认正序排序
      降序排序
      articles = session.query(Article).order_by(Article.create_time.desc()).all()
      降序，在字段前面加个符号代表降序
      articles = session.query(Article).order_by("-create_time").all()
      ```

```text
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import create_engine, String, Integer, Float, ForeignKey, DateTime, Date, Column, desc,asc
from sqlalchemy.dialects.mysql import LONGTEXT
from sqlalchemy.orm import sessionmaker,relationship,backref
from datetime import datetime

HOSTNAME = "127.0.0.1"
PORT = "3306"
USERNAME = "root"
PASSWORD = "123456"
DATABASE = "xt_flask"
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)

engine = create_engine(DB_URI)
Base = declarative_base(engine)
session = sessionmaker(engine)()

class User(Base):
    __tablename__ = "user"
    id = Column(Integer,primary_key=True,autoincrement=True)
    username = Column(String(50),nullable=False)

class Article(Base):
    __tablename__ = 'article'
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    # 注意default里面的datetime.now，没有()
    create_time = Column(DateTime,nullable=False,default=datetime.now)
    uid = Column(Integer,ForeignKey('user.id'))

    # author = relationship("User",backref=backref("articles",order_by=create_time.desc()))
    author = relationship("User", backref=backref("articles"))

    # 排序
    __mapper_args__ = {
        "order_by":create_time.desc(),
    }

    # 重写函数
    def __repr__(self):
        return "<Article(title:{},create_time:{})>".format(self.title,self.create_time)


# Base.metadata.drop_all()
# Base.metadata.create_all()
# 添加数据
# article1 = Article(title="title1")
# article2 = Article(title="title2")
# user = User(username='miku')
# user.articles = [article1,article2]
# session.add(user)
# session.commit()
# -----------------------------------
# article1 = Article(title="angle1")
# user = User(username="miku")
# user.articles = [article1]
# session.add(user)
# session.commit()
#
# import time
# time.sleep(2)
#
# article2 = Article(title="angle2")
# user.articles.append(article2)
# session.commit()


# 默认正序排序
# 降序排序
# articles = session.query(Article).order_by(Article.create_time.desc()).all()
# 降序，在字段前面加个符号代表降序
# articles = session.query(Article).order_by("-create_time").all()

articles = session.query(Article).all()
for article in articles:
    print(article)

user = session.query(User).first()
print(user.articles)
```

