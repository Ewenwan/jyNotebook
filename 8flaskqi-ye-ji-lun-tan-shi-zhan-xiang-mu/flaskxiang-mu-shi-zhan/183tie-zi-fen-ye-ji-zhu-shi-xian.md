### 1.相关链接

flask Paginate:[https://flask-paginate.readthedocs.io/en/latest/](https://flask-paginate.readthedocs.io/en/latest/)

### 2.添加测试数据

```
# 添加测试帖子数据
@manager.command
def create_test_post():
    for i in range(1,205):
        title = "标题{}".format(i)
        content = "内容:{}".format(i)
        board = BoardModel.query.first()
        author = FrontUser.query.first()
        post = PostModel(title=title,content=content)
        post.board = board
        post.author = author
        db.session.add(post)
        db.session.commit()
    print("添加帖子测试完成")
```

### 3.安装

```
pip install flask_paginate
```

### 4.参数

```
found：搜索时使用

* page：当前页面

per_page：一页上显示的记录数

page_parameter：包含页面索引的GET参数的名称（字符串）。如果您想同时迭代多个分页对象，请使用它。defautl是'page'。

per_page_parameter：一个名字per_page喜欢page_parameter。默认为'per_page'。

* inner_window：当前页面有多少链接

* outer_window：第一个/最后一个链接附近有多少个链接

prev_label：上一页的文字，默认为'＆laquo;'

next_label：下一页的文字，默认为'＆raquo;'

search：搜索与否？

total：分页记录总数

display_msg：pagation信息的文本

search_msg：搜索信息的文本

record_name：记录名称显示在分页信息中

link_size：页面链接的字体大小

alignment：分页链接的对齐方式

href：为链接添加自定义href - 这支持使用post方法的表单。必须包含{0}才能格式化页码

show_single_page：决定单个页面是否返回分页

bs_version：bootstrap的版本，默认为2

css_framework：css框架，默认为'bootstrap'

anchor：anchor参数，追加到页面href

format_total：数字格式总计，如1,234，默认为False

format_number：数字格式的开始和结束，如1,234，默认为False
```

### 5.初始化对象

```
# 获取page页数参数    
page = request.args.get(get_page_parameter(),type=int,default=1

# 传入页数参数，数据的总条数
pagination = Pagination(
    bs_version=3,page=page,
    total=PostModel.query.count(),
    outer_window=0,
    inner_window=2,
    )
```

### 6.每页数据

```
    offset = (page-1) * config.PER_PAGE
    count = offset + config.PER_PAGE
    # 从第几条开始显示第end条数据
    posts = PostModel.query.slice(offset,count)
```

### 7.前端

```
                <ul class="post-list-group">
                    {% for post in posts %}
                        <li>
                            <div class="author-avatar-group">
                                <img src="{{ post.author.avatar or url_for('static',filename="common/images/logo.png") }}"
                                     alt="">
                            </div>
                            <div class="post-info-group">
                                <p class="post-title">{{ post.title }}</p>
                                <p class="post-info">
                                    <span>作者:{{ post.author.username }}</span>
                                    <span>发表时间:{{ post.create_time }}</span>
                                    <span>评论:0</span>
                                    <span>阅读:0</span>
                                </p>
                            </div>
                        </li>
                    {% endfor %}
                </ul>
                <div style="text-align: center">
                    {{ pagination.links }}
                </div>
```

### 8.小细节

```
paginate.links 可以自动完成点击的模块
```



