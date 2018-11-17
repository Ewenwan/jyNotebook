### 1.帖子加精和取消加精视图函数

```
# 帖子加精
@bp.route('/hpost/',methods=['POST'])
@login_required
@permission_requeired(CMSPersmission.POSTER)
def hpost():
    post_id = request.form.get("post_id")
    if not post_id:
        return restful.params_error("请传入帖子id！")
    post = PostModel.query.get(post_id)
    if not post:
        return restful.params_error("没有这篇帖子！")
    highlight = HighlightPostModel()
    highlight.post = post
    db.session.add(highlight)
    db.session.commit()
    return restful.success()

@bp.route('/uhpost/',methods=["POST"])
@login_required
@permission_requeired(CMSPersmission.POSTER)
def uhpost():
    post_id = request.form.get("post_id")
    if not post_id:
        return restful.params_error("请传入帖子id！")
    post = PostModel.query.get(post_id)
    if not post:
        return restful.params_error("没有这篇帖子！")
    highlight = HighlightPostModel.query.filter_by(post_id=post_id).first()
    db.session.delete(highlight)
    db.session.commit()
    return restful.success()
```

### 2.获取帖子信息

```
# 权限判断，防止跨越访问
@bp.route('/posts/')
@login_required
@permission_requeired(CMSPersmission.POSTER)
def posts():
    # posts_list = PostModel.query.all()
    page = request.args.get(get_page_parameter(),type=int,default=1)
    offset = (page-1) * config.PER_PAGE
    count = offset + config.PER_PAGE
    posts_list = PostModel.query.slice(offset,count)
    total = PostModel.query.count()
    pagination = Pagination(bs_version=3,page=page,total=total,outer_window=0,inner_window=2)
    context = {
        "posts":posts_list,
        "pagination":pagination,
    }

    return render_template('cms/posts.html',**context)
```

### 3.把数据呈现在前端

```
{% extends 'cms/base.html' %}
{% from "common/_macros.html" import static %}

{% block title %}
    帖子管理
{% endblock %}

{% block head %}
    <script src="{{ static("cms/js/posts.js") }}"></script>
{% endblock %}

{% block page_title %}
    {{ self.title() }}
{% endblock %}

{% block main_content %}
    <table class="table table-bordered">
        <thead>
        <tr>
            <th>标题</th>
            <th>发布时间</th>
            <th>模块</th>
            <th>作者</th>
            <th>操作</th>
        </thead>
        <tbody>
        {% for post in posts %}
            <tr data-id="{{ post.id }}" data-highlight="{{ 1 if post.highlight else 0 }}">
                <td>
                    <a target="_blank" href="{{ url_for("front.post_detail",name=post.author.username,post_id=post.id) }}">{{ post.title }}</a>
                </td>
                <td>{{ post.create_time }}</td>
                <td>{{ post.board.name }}</td>
                <td>{{ post.author.username }}</td>
                <td>
                    {% if  post.highlight %}
                        <button class="btn btn-warning btn-xs highlight-btn" >取消加精</button>
                    {% else %}
                        <button class="btn btn-default btn-xs highlight-btn">加精</button>
                    {% endif %}
                        <button class="btn btn-danger btn-xs">移除</button>

                </td>
            </tr>
        {% endfor %}
        </tbody>
    </table>
    <div style="text-align: center;">
        {{ pagination.links }}
    </div>
{% endblock %}
```

### 4.ajax异步处理

```
$(function () {
    $('.highlight-btn').click(function (event) {
        event.preventDefault();

        var self = $(this);
        var tr = self.parent().parent();
        var post_id = tr.attr("data-id");
        var highlight = parseInt(tr.attr("data-highlight"));
        var url = ""
        if(highlight){
            url = '/cms/uhpost/';
        }else{
            url = '/cms/hpost/';
        }
        zlajax.post({
            'url':url,
            'data':{
                'post_id':post_id,
            },
            'success':function (data) {
                if(data["code"] == 200){
                    zlalert.alertSuccessToast("操作成功!");
                    setTimeout(function () {
                        window.location.reload();
                    },500);
                }else{
                    zlalert.alertInfo(data["message"]);
                }
            },
            'fail':function () {
                zlalert.alertNetworkError();
            }
        });
    });
});
```



