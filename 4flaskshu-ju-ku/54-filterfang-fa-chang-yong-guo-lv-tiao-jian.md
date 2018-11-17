# 54 filter方法常用过滤条件

过滤是数据库的一个很重要的功能，以下对一些常用的过滤条件进行解释，并且这些过滤条件都是只能通过filter方法实现的

如果想看底层sql原生语句，在语句末尾不加all\(\)，就可以打印出原生sql语句

1.equals

```text
article = session.query(Article).filter(Article.id == 1).first()
print(article)
```

2.not equals

```text
article = session.query(Article).filter(Article.title != 'title0').all()
print(article)
```

3.like & ilike\(不区分大小写\)

```text
rticles = session.query(Article).filter(Article.title.like('%title%')).all()
# 不分区大小写
articles = session.query(Article).filter(Article.title.ilike('%title%')).all()
print(articles)
```

4.in

```text
articles = session.query(Article).filter(Article.title.in_(['title1','title2'])).all()
print(articles)
```

5.not in

```text
icles = session.query(Article).filter(~Article.title.in_(['title1'])).all()
# articles = session.query(Article).filter(Article.title.notin_(['title1'])).all()
print(articles)
```

6.is null

```text
session.query(Article).filter(Article.content == None).all()
print(articles)
```

7.is not null

```text
articles = session.query(Article).filter(Article.content != None).all()
print(articles)
```

8.or

```text
articles = session.query(Article).filter(or_(Article.title=='title0',Article.content=='123')).all()
print(articles)
```

9.and

```text
rticles = session.query(Article).filter(Article.title=='title0' and Article.content == '123').all()
articles = session.query(Article).filter(and_(Article.title=='title0',Article.content == '123')).all()
print(articles)
```

```text
from sqlalchemy import create_engine, Column, Integer, Text, String, DateTime, String, Float, func,and_,or_
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
    content = Column(Text)

    def __repr__(self):
        return "<Article(title:%s)>" % self.title

# session.query(Article).filter(Article.id)
# 筛选关键字
# session.query(Article).filter_by(id=1)

# 1.equal
# article = session.query(Article).filter(Article.id == 1).first()
# print(article)

# # 2.not equal
# article = session.query(Article).filter(Article.title != 'title0').all()
# print(article)

# # 3. like
# articles = session.query(Article).filter(Article.title.like('%title%')).all()
# # 不分区大小写
# articles = session.query(Article).filter(Article.title.ilike('%title%')).all()
# print(articles)

# #  4. in
# articles = session.query(Article).filter(Article.title.in_(['title1','title2'])).all()
# print(articles)

# # 5. not in & ~
# articles = session.query(Article).filter(~Article.title.in_(['title1'])).all()
# # articles = session.query(Article).filter(Article.title.notin_(['title1'])).all()
# print(articles)

# # 6. is null
# articles = session.query(Article).filter(Article.content == None).all()
# print(articles)

# # 7. is not null
# articles = session.query(Article).filter(Article.content != None).all()
# print(articles)

# # 8. and
# # articles = session.query(Article).filter(Article.title=='title0' and Article.content == '123').all()
# articles = session.query(Article).filter(and_(Article.title=='title0',Article.content == '123')).all()
# print(articles)

# 9. or
articles = session.query(Article).filter(or_(Article.title=='title0',Article.content=='123')).all()
print(articles)
```

