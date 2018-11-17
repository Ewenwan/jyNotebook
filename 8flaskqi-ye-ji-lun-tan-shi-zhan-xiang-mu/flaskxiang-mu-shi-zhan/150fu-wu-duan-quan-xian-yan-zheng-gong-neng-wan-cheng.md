创建所有版块的视图

```
# 权限判断，防止跨越访问
@bp.route('/posts/')
@login_required
@permission_requeired(CMSPersmission.POSTER)
def posts():
    return render_template('cms/posts.html')

@bp.route('/comments/')
@login_required
@permission_requeired(CMSPersmission.COMMENTER)
def comments():
    return render_template('cms/comments.html')

@bp.route('/boards/')
@login_required
@permission_requeired(CMSPersmission.BOARDER)
def boards():
    return render_template('cms/boards.html')

@bp.route('fusers')
@login_required
@permission_requeired(CMSPersmission.FRONTUSER)
def fusers():
    return render_template('cms/fusers.html')

@bp.route('/cusers/')
@login_required
@permission_requeired(CMSPersmission.CMSUSER)
def cusers():
    return render_template('cms/cusers.html')

@bp.route('/croles/')
@login_required
@permission_requeired(CMSPersmission.ALL_PERMISSION)
def croles():
    return render_template('cms/croles.html')
```

为了防止跨越权限访问，还需要做一层验证

```
# 权限验证
def permission_requeired(permission):
    def outter(func):
        @wraps(func)
        def inner(*args,**kwargs):
            user = g.cms_user
            # 判断用户是否具有访问权限
            if user.has_permission(permission):
                return func(*args,**kwargs)
            else:
                return redirect(url_for('cms.index'))
        return inner
    return outter
```

这里所进行的验证，是基于原来的规定的功能的二进制码，进行与或运算判断是否具有相应的访问权限



