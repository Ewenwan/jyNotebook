### 1.相关链接

标签:[https://v3.bootcss.com/components/\#labels](https://v3.bootcss.com/components/#labels)

### 2.点击切换按钮特效

st参数为sort排序，board\_id参数为指定版块

```
                <ul class="nav nav-pills">
                    {% if current_sort == 1 %}
                        <li role="presentation" class="active"><a href="{{ url_for("front.index",st=1,board_id=current_board) }}">最新</a></li>
                    {% else %}
                        <li role="presentation"><a href="{{ url_for("front.index",st=1,board_id=current_board) }}">最新</a></li>
                    {% endif %}
                    {% if current_sort == 2 %}
                        <li role="presentation" class="active"><a href="{{ url_for("front.index",st=2,board_id=current_board) }}">精华帖子</a></li>
                    {% else %}
                        <li role="presentation"><a href="{{ url_for("front.index",st=2,board_id=current_board) }}">精华帖子</a></li>
                    {% endif %}
                    {% if current_sort == 3 %}
                        <li role="presentation" class="active"><a href="{{ url_for("front.index",st=3,board_id=current_board) }}">点赞最多</a></li>
                    {% else %}
                        <li role="presentation"><a href="{{ url_for("front.index",st=3,board_id=current_board) }}">点赞最多</a></li>
                    {% endif %}
                    {% if current_sort == 4 %}
                        <li role="presentation" class="active"><a href="{{ url_for("front.index",st=4,board_id=current_board) }}">评论最多</a></li>
                    {% else %}
                        <li role="presentation"><a href="{{ url_for("front.index",st=4,board_id=current_board) }}">评论最多</a></li>
                    {% endif %}

                </ul>
```

### 3.排序&版块过滤

```
@bp.route('/')
def index():
    sort = request.args.get("st",type=int,default=1) # 排序
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
    query_obj = None

    if sort == 1:
        # 最新
        query_obj = PostModel.query.order_by(PostModel.create_time.desc())
    elif sort == 2:
        # 按加精时间倒序排序
        # 两个表连接查询需要使用db.session()
        query_obj = db.session.query(PostModel).outerjoin(HighlightPostModel).order_by(HighlightPostModel.create_time.desc(),PostModel.create_time.desc())
    elif sort == 3:
        # 按照点赞数量排序
        query_obj = db.session.query(PostModel).outerjoin(LikePostModel).order_by(LikePostModel.like_num.desc(),PostModel.create_time.desc())
    elif sort == 4:
        query_obj = db.session.query(PostModel).outerjoin(CommentModel).group_by(PostModel.id).order_by(func.count(CommentModel.id).desc(),PostModel.create_time.desc())

    if board_id:
        # 按照版块筛选
        query_obj = PostModel.query.filter(PostModel.board_id==board_id)
        posts = query_obj.slice(offset,count)
        total = query_obj.count()
    else:
        posts = query_obj.slice(offset,count)
        total = query_obj.count()
    # 传入页数参数，数据的总条数
    pagination = Pagination(bs_version=3,page=page,total=total,outer_window=0,inner_window=2)
    context = {
        "boards":boards,
        "banners":banners,
        'posts':posts,
        'pagination':pagination,
        'current_board':board_id,
        'current_sort':sort,
        'like_obj':db.session.query(LikePostModel).outerjoin(PostModel),
    }
    return render_template("front/index.html",**context)
```



