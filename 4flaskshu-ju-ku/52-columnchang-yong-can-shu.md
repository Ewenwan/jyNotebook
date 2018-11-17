# 52 Column常用参数

* default:设置某个字段的默认值。默认值可以为一个表达式或者变量，函数
* nullable:设置某个字段是否可空，默认值为True
* primary\_key:设置某个字段为主键
* unique:设置某个字段为唯一的字段，不允许有重复值，默认值为True
* autoincrement:设置这个字段为自动增长的
* name:指定orm模型中某个属性映射到表中的字段名，如果不指定，那么会使用这个属性的名字作为字段名。如果指定了，就会使用指定的这个值作为参数，这个参数也可以当做位置参数，在第1个参数来指定。

```text
title = Column(String(50),name="标题",nullable=False)
title = Column('标题',String(50),nullable=False)
```

* onupdate:在数据更新的时候会调用这个参数指定的值或函数，在第一次插入这条数据的时候，不会用onupdate的值，只会使用default的值，常用的就是"update\_time"（每次更新数据的时候都要更新的值）

```text
from sqlalchemy import create_engine,Column,Integer,String,DateTime,String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

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

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    # create_time = Column(DateTime,default=datetime.now())
    # read_count = Column(Integer,default=12)
    title = Column(String(50),name="标题",nullable=False)
    title = Column('标题',String(50),nullable=False)
    # telephone = Column(String(11),unique=True)
    update_time = Column(DateTime,onupdate=datetime.now,default=datetime.now)

Base.metadata.drop_all()
Base.metadata.create_all()

article = Article(title="angle")
session.add(article)
session.commit()

# article = session.query(Article).first()
# article.title = '123'
# print(article.title)
# session.commit()
```

