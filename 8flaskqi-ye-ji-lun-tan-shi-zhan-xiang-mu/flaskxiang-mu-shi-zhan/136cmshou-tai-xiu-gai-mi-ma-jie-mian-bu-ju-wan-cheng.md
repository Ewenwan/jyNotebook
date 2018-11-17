### 使用boostrap框架

地址:[https://v3.bootcss.com/css/\#buttons](https://v3.bootcss.com/css/#buttons)

```
按钮:<button type="button" class="btn btn-primary">（首选项）Primary</button>
```

```
表单:
  <div class="form-group">
    <div class="input-group">
      <span class="input-group-addon">旧密码</span>
      <input class="form-control" type="password" name="oldpwd" placeholder="请输入旧密码">
    </div>
  </div>
```

### 给类视图定义装饰器

```
class ResetPwdView(views.MethodView):

    # 给类视图定义装饰器
    decorators = [login_requeired,]
    .....
```



