# 53 query函数可查询的数据

1. 模型对象。指定查找这个模型中所有的对象
2. 模型中的属性。可以指定只查找某个模型的其中几个属性
3. 聚合函数
   * func.count:统计行的数量
   * func.avg:求平均值
   * func.max:求最大值
   * func.min:求最小值
   * func.sum:求和
4. 'func'上，其实没有任何聚合函数，但是因为底层做了一些魔术，只要mysql中有聚合函数，都可以通过func调用

```text
实例:session.query(func.avg(Arictle.title)).first()
```

```text
from sqlalchemy import create_engine,Column,Integer,String,DateTime,String,Float,func
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

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    price = Column(Float,nullable=False)

    def __repr__(self):
        return "<Article(title:%s)>" % self.title

# Base.metadata.drop_all()
# Base.metadata.create_all()

# for x in range(6):
#     article = Article(title='title%s'%x,price=random.randint(50,100))
#     print(article)
#     session.add(article)
# session.commit()

# 模型对象
# articles = session.query(Article).all()
# # for article in articles:
# #     print(article)
# print(articles)

# # 模型中的属性
# articles = session.query(Article.title,Article.price).all()
# print(articles)

# 聚合函数
count = session.query(func.count(Article.id)).first()
print(count)

avg = session.query(func.avg(Article.price)).first()
print(avg)

max = session.query(func.max(Article.price)).first()
print(max)

min = session.query(func.min(Article.price)).first()
print(min)

sum = session.query(func.sum(Article.price)).first()
print(sum)

print(func.sum(Article.title))
```

