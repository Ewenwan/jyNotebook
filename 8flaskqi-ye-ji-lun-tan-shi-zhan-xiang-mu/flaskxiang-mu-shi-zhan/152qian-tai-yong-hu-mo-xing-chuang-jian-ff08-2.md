定义添加数据的命令

```
# 在此之前需要映射front的模型到数据库中
# python manage.py db migrate
# python manage.py db upgrade
@manager.option('-t','--telephone',dest='telephone')
@manager.option('-u','--username',dest='username')
@manager.option('-p','--password',dest='password')
def create_front_user(telephone,username,password):
    user = FrontUser(telephone=telephone,username=username,password=password)
    db.session.add(user)
    db.session.commit()
```

```
# 前台用户测试数据
# python manage.py create_front_user -t 153556565-u angle -p 123456
```



