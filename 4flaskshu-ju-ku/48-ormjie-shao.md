# 48 ORM介绍

* 用“declarative\_base”根据"engine"创建一个ORM基类

```text
from sqlalchemy.ext.declarative import declarative_base

engine = create_engine(DB_URI)

Base = declarative_base(engine)
```

* 用这个"Base"类作为基类来写自己的ORM类。要定义"\_\__tablename_\_\_"类属性，来指定这个模型映射到数据库中的表名

```text
class Person(Base):
    __tablename__ = "person"
```

* 创建需要在表中映射的字段，所有需要映射到表中的属性都应为Column类型

```text
class Person(Base):
    __tablename__ = "person"
    # 2.要在这个ORM模型中创建一些属性，来跟表中的字段进行一一映射。这些属性必须是SQLAlchemy给我们提供好的数据类型
    # Column()对象
    id = Column(Integer,primary_key=True,autoincrement=True)
    # String(50)==>varchar(50)
    name = Column(String(50))
    age = Column(Integer)
```

* 使用"Base.metadata.create\_all\(\)"来创建表，将模型映射到数据库中
* 一旦使用"Base.metadata.create\_all\(\)"将模型映射到数据库中后，即使改变了模型的字段，也不会重新映射了

```text
from sqlalchemy import create_engine,Column,Integer,String
from sqlalchemy.ext.declarative import declarative_base

HOSTNAME = "127.0.0.1"
PORT = "3306"
DATABASE = "xt_flask"
USERNAME = "root"
PASSWORD = "123456"
DB_URI = "mysql+pymysql://{USERNAME}:{PASSWORD}@{HOSTNAME}:{PORT}/{DATABASE}?charset=utf8".format(
    USERNAME=USERNAME,
    PASSWORD=PASSWORD,
    HOSTNAME=HOSTNAME,
    PORT=PORT,
    DATABASE=DATABASE)

engine = create_engine(DB_URI)
# 类工厂函数，返回的是一个基类
Base = declarative_base(engine)

# conn = engine.connect()
# rs =  conn.execute("select 1")
# print(rs.fetchone())

# create table person(id int primary key autoincrement,name varchar(50),age int)

# 1.创建一个OMR模型，这个ORM蘑菇型必须继承自SQLAlchemy给我们提供好的基类
class Person(Base):
    # 数据库中的表名
    __tablename__= "person"
# 2.要在这个ORM模型中创建一些属性，来跟表中的字段进行一一映射。这些属性必须是SQLAlchemy给我们提供好的数据类型
    # Column()对象
    id = Column(Integer,primary_key=True,autoincrement=True)
    # String(50)==>varchar(50)
    name = Column(String(50))
    age = Column(Integer)
# 3.将创建好的ORM模型，映射到数据库中

Base.metadata.create_all()
```

