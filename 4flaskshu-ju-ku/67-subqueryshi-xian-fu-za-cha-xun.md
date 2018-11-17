# 67 subquery实现复杂查询

## 子查询

子查询可以让多个查询变成一个查询，只要查找一次数据库，性能相对来讲更加高效一点，不用写多个sql语句就可以一些复杂的查询了，那么在sqlalchemy中，要实现一个子查询，应该使用以下几个步骤:

1.将子查询按照传统的方式写好查询代码，然后在"query"对象后面执行"subquery"方法，将这个查询变成一个子查询

```text
user = session.query(func.max(User.age).label("age")).subquery()
```

2.在子查询中，将以后需要用到的字段通过"label"方法，取个别名

```text
 session.query(func.max(User.age).label("age"))
```

3.在父查询中，如果想要使用子查询的字段，那么可以通过子查询的变量上的"c"属性拿到

```text
result = session.query(User).filter(User.age == user.c.age).all()
```

## 完整代码

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
    city = Column(String(50),nullable=False)
    age = Column(Integer,default=0)

    def __repr__(self):
        return "<User(username:%s)>" % self.username

# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user1 = User(username="A",city="M城",age=15)
# user2 = User(username="B",city="G城",age=21)
# user3 = User(username="C",city="H城",age=12)
# user4 = User(username="D",city="J城",age=20)
#
# session.add_all([user1,user2,user3,user4])
# session.commit()

# # mysql> select * from user where age = 21;
user = session.query(func.max(User.age).label("age")).subquery()
result = session.query(User).filter(User.age == user.c.age).all()
print(result)

# # 实现子查询
# subuser = session.query(User.city.label("city"),User.age.label("age")).filter(User.username == 'A').subquery()
# # subquery.column.city == subquery.c.city
# result = session.query(User).filter(User.city == subuser.c.city).all()
# print(result)
```

