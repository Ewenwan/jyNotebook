定义添加帖子的表单

```
class AddPostForm(BaseForm):
    title = StringField(validators=[InputRequired(message="请输入标题！")])
    content = StringField(validators=[InputRequired(message="请输入内容！")])
    board_id = IntegerField(validators=[InputRequired(message="请输入板块id！")])
```

验证是否登录

```
from flask import session,redirect,url_for,g
from functools import wraps
import config

# @wraps(func)，将参数包装起来，避免数据丢失

# 登录验证判断
def login_required(func):
    @wraps(func)
    def inner(*args,**kwargs):
        if config.FRONT_USER_ID in session:
           return func(*args,**kwargs)
        else:
            return redirect(url_for('cms.login'))
    return inner

```

视图函数\*\*添加帖子

```
@bp.route('/apost/',methods=['GET','POST'])
@login_required
def apost():
    if request.method == "GET":
        return render_template('front/apost.html')
    else:
        form = AddPostForm(request.form)
        if form.validate():
            title = form.title.data
            content = form.content.data
            board_id = form.board_id.data
            board = BoardModel.query.get(board_id)
            if not board:
                return restful.params_error(message="没有这个模块！")
            post = PostModel(title=title,content=content)
            post.board = board
            db.session.add(post)
            db.session.commit()
            return  restful.success()
        else:
            return restful.params_error(message=form.get_error())
```



