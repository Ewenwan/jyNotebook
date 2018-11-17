# 66 join实现复杂查询

join查询分为两种，一种是inner join,另一种是outer join。默认的是inner join,如果指定left join或者是right join则为outer join。如果想要查询User及其对应的Address，则可以通过以下方式来实现:

```text
for u,a in session.query(User,Address).filter(User.id == Address.user_id).all()
    print u
    print a
```

tips:join方法配合filter过滤方法一起使用

left join:

```text
result = session.query(User).join(Article).group_by(User.id).order_by(func.count(Article.id).desc()).all()
```

right join:

```text
result = session.query(Article).join(User).group_by(User.id).order_by(func.count(Article.id).desc()).all()
```

outer join:

```text
result = session.query(Article).outerjoin(User).group_by(User.id).order_by(func.count(Article.id).desc()).all()
```

```text
注意:在sqlalchemy中，使用join来完成内连接，在写join的时候，如果不写join的条件，那么默认将使用外键来作为条件连接
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

    def __repr__(self):
        return "<User(id:%s,username:%s)>" % (self.id,self.username)

class Article(Base):
    __tablename__ = 'article'
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    create_time = Column(DateTime,nullable=False,default=datetime.now)
    uid = Column(Integer,ForeignKey("user.id"))

    author = relationship("User",backref=backref("articles"))

    def __repr__(self):
        return "<Article(title:%s)>" % self.title

# 添加数据
# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user1 = User(username="angle")
# user2 = User(username="miku")
#
# for i in range(1):
#     article = Article(title="title1 %s" % i)
#     article.author = user1
#     session.add(article)
# session.commit()
#
# for i in range(1,3):
#     article = Article(title="title1 %s" % i)
#     article.author = user2
#     session.add(article)
# session.commit()

# 找到所有的用户，按照发表的文章数量进行排序
# 默认会使用外键作为连接条件
# select user.username,count(article.id) fro m user join article on user.id = article.uid group by user.id order by count(article.id) desc;
# result = session.query(User.username,func.count(Article.id)).outerjoin(Article,User.id==Article.id).group_by(User.id).order_by(func.count(Article.id).desc()).all()

# # 左外连接
# result = session.query(User).join(Article).group_by(User.id).order_by(func.count(Article.id).desc()).all()
# # # 右外连接,注意类和left的类位置，调换
# result = session.query(Article).join(User).group_by(User.id).order_by(func.count(Article.id).desc()).all()
# # # outerjoin
# result = session.query(Article).outerjoin(User).group_by(User.id).order_by(func.count(Article.id).desc()).all()
# print(result)
```

