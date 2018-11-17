# 50 SQLAlchemy对数据的增删改查操作

1.构建session对象，所有和数据库的ORM操作必须通过一个叫做"session"的会话对象来实现，通过以下代码来获取会话对象:

```text
from sqlalchemy.orm import sessionmaker

# Session = sessionmaker(engine)
# session = Session()
# 上面两行等价于下面一行
session = sessionmaker(engine)()
```

2.添加对象

* 创建对象，也即创建一条数据

```text
p = Person(name="angle",age=16,country="china")
```

* 将对象添加到'session'会话对象中

```text
session.add(p)
```

* 将session中的对象做commit操作\(提交\)

```text
session.commit()
```

* 一次性添加多条数据

```text
p1 = Person(name="angle1",age=16,country="china")
p2 = Person(name='angle2',age=20,country='china')
session.add_all([p1,p2])
```

3.查改对象

```text
#查找某个模型对应的那个表中所有的数据:
all_person = session.query(Person).all()

# 使用filter_by来做条件查询
all_person = session.query(Person).filter_by(name='angle1').all()

# 使用filter来做条件查询
all_person = session.query(Person).filter(Person.name.contains('angle'))

#使用get方法查找数据，get方法是根据id来查询的，只会返回一条数据或者None
person = session.query(Person).get(primary_key)

#使用first方法获取结果集中的第一条数据
person = session.query(Person).first()
```

4.修改对象，首先在数据库查找数据，然后将数据进行修改，最后做commit操作

```text
person = session.query(Person).first()
person.name = 'angle_update'
session.commit()
```

5.删除对象，首先在数据库查找数据，然后将查找到的数据进行删除，最后执行commit操作

```text
person = session.query(Person).first()
session.delete(person)
session.commit()
```

```text
from sqlalchemy import create_engine,Column,String,Integer
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

HOSTNAME = '127.0.0.1'
PORT = "3306"
USERNAME = "root"
PASSWORD = "123456"
DATABASE = "xt_flask"
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)

engine = create_engine(DB_URI)

Base = declarative_base(engine)

# Session = sessionmaker(engine)
# session = Session()
# 上面两行等价于下面一行
session = sessionmaker(engine)()

class Person(Base):
    __tablename__ = "person"
    id = Column(Integer,primary_key=True,autoincrement=True)
    # String(50)==>varchar(50)
    name = Column(String(50))
    age = Column(Integer)
    country = Column(String(50))

    # 返回字符串
    def __str__(self):
        return "<Person(name:%s,age:%s,country:%s)>" % (self.name,self.age,self.country)

# session会话

# 增
def add_data():
    p = Person(name="angle", age=16, country="china")
    p1 = Person(name="angle1",age=16,country="china")
    p2 = Person(name='angle2',age=20,country='china')
    session.add_all([p1,p2])
    # session.add(p)
    session.commit()

# 查
def serach_data():
    # # 指定表，all()方法返回所有数据
    # all_person = session.query(Person).all()
    # # print(all_person)
    # for p in all_person:
    #     print(p)

    # 指定筛选
    # all_person = session.query(Person).filter_by(name='angle1').all()
    # for p in all_person:
    #     print(p)

    # # filter(条件)
    # all_person = session.query(Person).filter(Person.name.contains('angle'))
    # for p in all_person:
    #     print(p)

    # # 获取id为1的数据
    # person = session.query(Person).get(1)
    # print(person)

    #使用first方法获取结果集中的第一条数据
    person = session.query(Person).first()
    print(person)

# 改
def update_data():
    person = session.query(Person).first()
    person.name = 'angle_update'
    session.commit()

# 删
def delete_data():
    person = session.query(Person).first()
    session.delete(person)
    session.commit()

if __name__ == "__main__":
    # Base.metadata.create_all()
    # add_data()
    # serach_data()
    # update_data()
    delete_data()
```

