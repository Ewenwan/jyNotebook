验证更改密码的表单

```
class ResetpwdForm(BaseForm):
    oldpwd = StringField(validators=[Length(6,20,message="请输入正确格式的密码")])
    newpwd = StringField(validators=[Length(6,20,message="请输入正确格式的密码")])
    newpwd2 = StringField(validators=[EqualTo("newpwd")])
```

判断更改密码的信息

```
    def post(self):
        form = ResetpwdForm(request.form)
        if form.validate():
            # 获取密码信息
            oldpwd = form.oldpwd.data
            newpwd = form.newpwd.data
            # 获取全局对象g的用户属性
            user = g.cms_user
            # 判断原密码是否一致
            if user.check_password(oldpwd):
                # 修改密码
                user.password = newpwd
                # 提交到数据库中
                db.session.commit()
                # 返回数据
                return jsonify({"code":200,"message":""})
            else:
                return jsonify({"code":400,"message":"旧密码错误"})
        else:
            message = form.get_error()
            return jsonify({'code':400,"message":message})
```



