修改视图，判断并过滤属于哪个板块的

```
@bp.route('/')
def index():
    board_id = request.args.get("board_id",type=int,default=None)
    boards = BoardModel.query.all()
    banners = BannerModel.query.order_by(BannerModel.priority.desc(),BannerModel.create_time.desc()).limit(4)
    # posts = PostModel.query.all()
    page = request.args.get(get_page_parameter(),type=int,default=1)
    offset = (page-1) * config.PER_PAGE
    count = offset + config.PER_PAGE
    # 从第几条开始显示第end条数据
    # posts = PostModel.query.slice(offset,count)
    posts = None
    total = 0
    if board_id:
        query_obj = PostModel.query.filter_by(board_id=board_id)
        posts = query_obj.slice(offset,count)
        total = query_obj.count()
    else:
        posts = PostModel.query.slice(offset,count)
        total = PostModel.query.count()
    # 传入页数参数，数据的总条数
    pagination = Pagination(bs_version=3,page=page,total=total,outer_window=0,inner_window=2)
    context = {
        "boards":boards,
        "banners":banners,
        'posts':posts,
        'pagination':pagination,
        'current_board':board_id,
    }
    return render_template("front/index.html",**context)
```

前端中判断是否被选中

```
<div class="list-group">
                {% if current_board %}
                    <a href="/" class="list-group-item">所有版块</a>
                {% else %}
                     <a href="/" class="list-group-item active">所有版块</a>
                {% endif %}
                {% for board in boards %}
                    {% if board.id == current_board %}
                        <a href="{{ url_for("front.index",board_id = board.id) }}" class="list-group-item active">{{ board.name }}</a>
                    {% else %}
                        <a href="{{ url_for("front.index",board_id = board.id) }}" class="list-group-item">{{ board.name }}</a>
                    {% endif %}
                {% endfor %}
```



