### 1.相关链接

表单:https://v3.bootcss.com/css/\#tables

### 2.发表帖子页面

```
{% extends "front/base.html" %}
{% from "common/_macros.html" import static%}

{% block title %}
    发布帖子
{% endblock %}

{% block head %}
    <script src="{{ static("ueditor/ueditor.config.js") }}"></script>
    <script src="{{ static("ueditor/ueditor.all.min.js") }}"></script>
    <script src="{{ static("front/js/apost.js") }}"></script>
{% endblock %}

{% block body %}
    <form action="" method="post">
        <div class="form-group">
            <div class="input-group">
                <span class="input-group-addon">标题</span>
                <input type="text" class="form-control" name="title">
            </div>
            <div class="form-group">
                <div class="input-group">
                    <span class="input-group-addon">版块</span>
                    <select name="board_id" class="form-control">
                        {% for board in boards %}
                            <option value="{{ board.id }}">{{ board.name }}</option>
                        {% endfor %}
                    </select>
                </div>
            </div>
        </div>
        <div class="form-group">
            <script id="editor" type="text/plain" style="height: 600px;"></script>
        </div>
        <div class="form-group">
            <a href="{{ url_for("front.apost") }}" class="btn btn-danger">发布帖子</a>
        </div>
    </form>
{% endblock %}
```



