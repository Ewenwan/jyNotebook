# 64 数据查询懒加载技术

在一对多，或者多对多的时候，如果想要获取多的这一部分的数据的时候，往往能通过一个属性就可以全部获取了。比如有一个作者，想要或者这个作者的所有文章，那么可以通过user,articles就可以获取所有的。但有时候我们不想获取所有的数据，比如只想获取这个作者今天发表的文章，那么这时候我们可以给relationship传递一个lazy="dynamic"，以后通过user,articles获取到的就不是一个列表，而是一个AppendQuery对象了。这样就可以对这个对象再进行一层过滤和排序等操作

通过lazy="dynamic"，获取出来的多的那一部分的数据，就是一个’AppenderQuery‘对象了。这种对象既可以添加新数据，也可以跟"Query"一样，可以再进行一层过滤，总而言之，如果在获取数据的时候，想要对多的那一边的数据再进行一层过滤，那么这时候就可以考虑使用lazy='dynamic'

```text
author = relationship("User",backref=backref('articles',lazy="dynamic"))
```

```text
# 添加数据
# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user = User(username = "angle")
# for i in range(100):
#     article = Article(title="title {}".format(i))
#     article.author = user
#     session.add(article)
#     session.commit()

from sqlalchemy.orm.collections import  InstrumentedList
from sqlalchemy.orm.dynamic import AppenderQuery
from sqlalchemy.orm.query import Query
user = session.query(User).first()
# print(user.articles.all())
# Query对象,所有id大于50的数据
# print(user.articles.filter(Article.id > 50).all())
#  可以继续追加数据进去
article = Article(title="title 101")
user.articles.append(article)
session.commit()
```

