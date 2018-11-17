# 63 limit、offset以及切片操作

1. limit:可以限制每次查询的时候只查询几条数据。
   1. ```text
      获取前10条数据
      articles = session.query(Article).limit(10).all()
      ```
2. offset:可以限制查找数据的时候过来前面多少条。
   1. ```text
      # select * from article limit 4 offset 9
      # select * from article limit 9,4
      # articles = session.query(Article).order_by(Article.id.desc()).offset(10).limit(10).all()
      # slice(limit,offset),desc()降序
      # articles = session.query(Article).order_by(Article.id.desc()).slice(0,10).all()
      ```
3. 切片:可以Query对象使用切片操作，来获取想要的数据
   1. ```text
      articles = session.query(Article).order_by(Article.id.desc())[0:10]
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

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    create_time = Column(DateTime,default=datetime.now)

    def __repr__(self):
        return "<Article(title:%s,create_time:%s)>" % (self.title,self.create_time)

# 添加数据
# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# for i in range(100):
#     title = "title %s" % i
#     article = Article(title=title)
#     session.add(article)
#     session.commit()

# 实战
# articles = session.query(Article).all()
# 获取前10条数据
# articles = session.query(Article).limit(10).all()
# offset(10)代表从第几条的数据开始
# select * from article limit 4 offset 9
# select * from article limit 9,4
# articles = session.query(Article).order_by(Article.id.desc()).offset(10).limit(10).all()
# slice(limit,offset),desc()降序
# articles = session.query(Article).order_by(Article.id.desc()).slice(0,10).all()
# 切片
articles = session.query(Article).order_by(Article.id.desc())[0:10]
print(articles)
```

