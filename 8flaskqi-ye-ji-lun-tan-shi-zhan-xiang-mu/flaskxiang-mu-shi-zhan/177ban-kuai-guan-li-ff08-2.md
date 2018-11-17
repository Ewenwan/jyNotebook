在主页添加模块

```
    <div class="sm-container">
        <div style="padding-bottom: 10px;">
            <button class="btn btn-warning btn-block">发表帖子</button>
        </div>
        <div class="list-group">
            <a href="#" class="list-group-item active">所有版块</a>
            {% for board in boards %}
                <a href="#" class="list-group-item">{{ board.name }}</a>
            {% endfor %}
        </div>
    </div>
```

![](/assets/177-01.png)主页视图

```
@bp.route('/boards/')
@login_required
@permission_requeired(CMSPersmission.BOARDER)
def boards():
    board_models = BoardModel.query.all()
    context = {
        "boards":board_models,
    }
    return render_template('cms/boards.html',**context)
```



