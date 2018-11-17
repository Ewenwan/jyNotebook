# 59 ORM层面删除数据注意事项

ORM层面删除数据，会无视mysql级别的外键约束，直接会对将对应的数据删除，然后将从表中的那个外键设置为NULL,如果想要避免这种行为，应该将从表中的外键的"nullable=False"

```text
class User(Base):
    __tablename__ = "user"
    id = Column(Integer,primary_key=True,autoincrement=True)
    username = Column(String(50),nullable=False)

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer,primary_key=True,autoincrement=True)
    title = Column(String(50),nullable=False)
    # 会起到限制
    uid = Column(Integer,ForeignKey('user.id'),nullable=False)
    # uid = Column(Integer,ForeignKey('user.id'))

    author = relationship("User",backref="articles")

# Base.metadata.drop_all()
# Base.metadata.create_all()
#
# user = User(username = 'angle1')
# article = Article(title = 'angle2')
#
# article.author = user
#
# session.add(article)
# session.commit()

user = session.query(User).first()
# 删除user表，article表的外键修改为null
session.delete(user)
session.commit()
```



