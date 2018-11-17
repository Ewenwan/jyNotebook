# 55 外键及其四种约束讲解

在MySQL中，外键可以让表之间的关系更加紧密，而SQLAlchemy同样支持外键。通过FpreignKey类来实现，并且可以指定表的外键约束。相关示例代码如下:

```text
from sqlalchemy import create_engine, Column, Integer, Text, String, 
DateTime, String, Float, func,and_,or_,ForeignKey

class User(Base):
    __tablename__ = 'user'
    id = Column(Integer,primary_key=True,autoincrement=True)
    username = Column(String(50),nullable=False)

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    content = Column(Text,nullable=False)

    # 外键
    uid = Column(Integer,ForeignKey("user.id"))

Base.metadata.drop_all()
Base.metadata.create_all()
```

外键约束有以下几项:

1. RESTRICT\(restrict\):父表数据被删除，会阻止删除
2. NO ACTION:在MySQL中，同RESTRICT
3. CASCADE:级联删除
4. SET NULL:父类数据被删除，子表数据设置为NULL

```text
from sqlalchemy import create_engine, Column, Integer, Text, String, DateTime, String, Float, func,and_,or_,ForeignKey
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
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

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    content = Column(Text,nullable=False)

    # 外键，没有指定，就默认为RESTRICT
    # RESTRICT:阻止删除数据
    # uid = Column(Integer,ForeignKey("user.id",ondelete="RESTRICT"))
    # 级联删除
    # uid = Column(Integer, ForeignKey("user.id", ondelete="CASCADE"))
    # 只有父表被删除，子表修改为NULL
    uid = Column(Integer, ForeignKey("user.id", ondelete="SET NULL"))

Base.metadata.drop_all()
Base.metadata.create_all()

user = User(username = 'angle')
session.add(user)
session.commit()

article = Article(content='abc',title='123',uid=1)
session.add(article)
session.commit()
```

