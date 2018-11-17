### 1.自定义404页面

```
{% from 'common/_macros.html' import static %}
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <title>该页面不存在喔</title>
    <meta name="keywords" content="" />
    <meta name="description" content="" />
    <link rel="stylesheet" href="{{ static('front/css/404.css') }}"/>
</head>
<body>
<div class="error wp960 auto">
    <div class="img">
        <img src="{{ url_for('static',filename='common/images/error.jpg') }}" />
    </div>
    <div><a class="back" href="/">返回首页</a></div>
</div>
</body>
</html>
```

### 2.自定义404视图

```
@app.errorhandler(404)
def page_not_found(e):
    return render_template('front/404.html'), 404
```

### 3.帖子详情页面

```
#@bp.route('/p/<post_id>/')
@bp.route('/<name>/<post_id>/')
def post_detail(name,post_id):
    post = PostModel.query.get(post_id)
    if not post:
        abort(404)
    return render_template('front/pdetail.html',post=post)
```

### 4.帖子页面

```
{% extends "front/base.html" %}

{% block title %}
    {{ post.title }}
{% endblock %}

{% block head %}
    <script src="{{ static('ueditor/ueditor.config.js') }}"></script>
    <script src="{{ static('ueditor/ueditor.all.min.js') }}"></script>
    <script src="{{ static('front/js/pdetail.js') }}"></script>
    <link rel="stylesheet" href="{{ url_for('static',filename="front/css/pdetail.css") }}">
{% endblock %}

{% block body %}
    <div class="lg-container">
                <div class="post-container">
            <h2>{{ post.title }}</h2>
            <p class="post-info-group">
                <span>发表时间：{{ post.create_time }}</span>
                <span>作者：{{ post.author.username }}</span>
                <span>所属板块：{{ post.board.name }}</span>
                <span>阅读数：{{ post.read_count }}</span>
                <span>评论数：0</span>
            </p>
            <article class="post-content" id="post-content" data-id="{{ post.id }}">
                {{ post.content|safe }}
            </article>
        </div>
    </div>
    <div class="sm-container">
    </div>
{% endblock %}
```



