### 添加轮播图管理

```
<li class="nav-group banner-manage"><a href="{{ url_for('cms.banners') }}">轮播图管理</a></li>
```

### 轮播图管理页面

```
{% extends 'cms/base.html' %}

{% block title %}
    轮播图管理
{% endblock %}

{% block head %}
    <style>
        .top-box{
            overflow: hidden;
            background-color: #ecedf0;
            {#padding:10px 5px;/*内边距，上下10px，左右5px*/#}
            padding:10px;/*内边距，上下左右10px*/
        }
    .top-box button{
        float:right;
    }
    </style>
{% endblock %}

{% block page_title %}
    {{ self.title() }}
{% endblock %}

{% block main_content %}
    <div class="top-box">
        <button class="btn btn-warning">
            添加轮播图
        </button>
    </div>
    <table class="table table-bordered">
        <tr>
            <th>名称</th>
            <th>图片链接</th>
            <th>跳转链接</th>
            <th>优先级</th>
            <th>创建时间</th>
            <th>操作</th>
        </tr>
    </table>
{% endblock %}
```



