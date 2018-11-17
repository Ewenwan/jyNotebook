在CMSUser模型上扩展判断权限的功能

```
    # 注意roles是什么，是上面的反向这个表的，用于通过这个属性绑定CMSRole模型
    # 拿到用户所有的权限
    @property
    def permissions(self):

        # 没有任何权限
        if not self.roles:
            return 0
        all_permissions = 0
        # 遍历权限
        for role in self.roles:
            permissions = role.permissions
            all_permissions |= permissions
        return all_permissions

    # 判断用户权限
    def has_permission(self,permission):
        # all_permissions = self.permissions
        # result =  all_permissions & permission == permission
        # return result
        return self.permissions & permission == permission

    # 判断是否为开发者
    def is_developer(self):
        return self.has_permission(CMSPersmission.ALL_PERMISSION)
```

定义为用户添加权限的命令

```
# 将用户添加到访问者权限中
# python manage.py add_user_to_role -e 1479852727@qq.com -n 访问者
# 定义添加角色的命令，不然没有访问权限
# 将某用户添加到某角色中
@manager.option('-e','--email',dest='email')
@manager.option('-n','--name',dest='name')
def add_user_to_role(email,name):
    user = CMSUser.query.filter_by(email=email).first()
    if user:
        role = CMSRole.query.filter_by(name=name).first()
        if role:
            role.users.append(user)
            db.session.commit()
            print("用户添加到角色成功")
        else:
            print("没有这个角色:{}".format(name))
    else:
        print("{}邮箱没有这个用户".format(email))


# python manage.py test_permission
@manager.command
def test_permission():
    # 查询用户
    user = CMSUser.query.first()
    if user.is_developer():
        print("拥有访问者权限")
    else:
        print("无访问者权限")
```



