# 65 group\_by和having子句

## group\_by

根据某个字段进行分组

## having:

having是对查找结果进一步过滤，在分组的基础上在进行筛选过滤

## 子查询

sqlalchemy支持子查询，比如现在要查找一个用户的用户名以及该用户的邮箱地址数量。要满足这个需求，可以在子查询中查找到所有用户的邮箱数（通过group by合并同一用户），然后再将结果放在父查询中进行使用:

```text
result = session.query(User.age,func.count(User.id)).group_by(User.age).having(User.age < 18).all()
print(result)
```

```text
from sqlalchemy import create_engine,Column,String,ForeignKey,Float,DateTime,Date,Integer,Enum,func
from sqlalchemy.ext.declarative import declarative_base
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
    age = Column(Integer,default=0)
    gender = Column(Enum("male","female","secret"))

    def __repr__(self):
        return "<Article(id:%s,username:%s)>" % (self.id.self.username)

# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user1 = User(username="angle",age=17,gender="male")
# user2 = User(username="miku",age=18,gender="male")
# user3 = User(username="xue",age=18,gender="female")
# user4 = User(username="yue",age=19,gender="female")
# user5 = User(username="mi",age=20,gender="female")
#
# session.add_all([user1,user2,user3,user4,user5])
# session.commit()

# 每个年龄段的人数
#  select count(*) from user group by age;
from sqlalchemy.orm.query import Query
# result = session.query(User.age,func.count(User.id)).group_by(User.age).all()
result = session.query(User.age,func.count(User.id)).group_by(User.age).having(User.age < 18).all()
print(result)
```

