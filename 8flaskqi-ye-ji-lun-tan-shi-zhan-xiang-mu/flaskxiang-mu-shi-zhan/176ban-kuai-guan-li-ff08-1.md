### 版块管理页面

```
{% extends 'cms/base.html' %}

{% block title %}
    版块管理
{% endblock %}

{% block head %}
    <script src="{{ url_for('static',filename='cms/js/boards.js') }}"></script>
{% endblock %}

{% block page_title %}
    {{  self.title() }}
{% endblock %}

{% block main_content %}
    <div class="top-box">
        <button class="btn btn-waring" style="float:right" id="add-board-btn">添加新版块</button>
    </div>
    <table class="table table-bordered">
        <thead>
            <tr>
                <th>版块名称</th>
                <th>帖子数量</th>
                <th>创建时间</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>
            {% for board in boards %}
                <tr>
                    <td>{{ board.name }}</td>
                    <td>0</td>
                    <td>{{ board.create_time }}</td>
                    <td>
                        <button class="btn btn-default btn-xs edit-board-tn">编辑</button>
                        <button class="btn btn-danger btn-xs delete-board-tn">删除</button>
                    </td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
{% endblock %}
```

### 添加js

```
$(function () {
    $("#add-board-btn").click(function (event) {
        event.preventDefault();

        zlalert.alertOneInput({
            'text':"请输入版块名称",
            'placeholder':"模块名称",
            'confirmCallback':function (inputValue) {
                zlajax.post({
                    'url':'/cms/aboard/',
                    'data':{
                        'name':inputValue,
                    },
                   'success':function (data) {
                        if(data['code'] == 200){
                            window.location.reload();
                        }else{
                            zlalert.alertInfo(data["message"]);
                        }
                   },
                    'fail':function () {
                        zlalert.alertNetworkError();
                    },
                });
            },
        });

    });
});
```

### 版块管理视图

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

# 添加版块
@bp.route('/aboard/',methods=['POST'])
@login_required
@permission_requeired(CMSPersmission.BOARDER)
def aboard():
    form = AddBoardForm(request.form)
    if form.validate():
        name = form.name.data
        board = BoardModel(name=name)
        db.session.add(board)
        db.session.commit()
        return restful.success()
    else:
        return restful.params_error(message=form.get_error())

# 编辑版块
@bp.route('/uboard/',methods=["POST"])
@login_required
@permission_requeired(CMSPersmission.BOARDER)
def uboard():
    form = UpdateBoardForm(request.form)
    if form.validate():
        board_id = form.board_id.data
        name = form.name.data
        board = BoardModel.query.get(board_id)
        if board:
            board.name = name
            db.session.commit()
            return restful.success()
        else:
            return restful.params_error(message="没有这个版块")
    else:
        return restful.params_error(message=form.get_error())

# 删除版块
@bp.route('/dboard/',methods=["POST"])
@login_required
@permission_requeired(CMSPersmission.BOARDER)
def dboard():
    board_id = request.form.get("board_id")
    if not board_id:
        return restful.params_error(message="请传入版块id！")
    board = BoardModel.query.get(board_id)
    if not board:
        return restful.params_error(message="没有这个版块！")
    db.session.delete(board)
    return restful.success()
```



