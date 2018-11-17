### 1.相关链接

轮播图的组件:https://v3.bootcss.com/javascript/\#carousel

### 2.轮播图模板

```
<div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
  <!-- Indicators -->
  <ol class="carousel-indicators">
    <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
    <li data-target="#carousel-example-generic" data-slide-to="1"></li>
    <li data-target="#carousel-example-generic" data-slide-to="2"></li>
  </ol>

  <!-- Wrapper for slides -->
  <div class="carousel-inner" role="listbox">
    <div class="item active">
      <img src="..." alt="...">
      <div class="carousel-caption">
        ...
      </div>
    </div>
    <div class="item">
      <img src="..." alt="...">
      <div class="carousel-caption">
        ...
      </div>
    </div>
    ...
  </div>

  <!-- Controls -->
  <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>
```

### 3.首页的轮播图完成

```
{% extends "front/base.html" %}
{% from "common/_macros.html" import static%}

{% block title %}
    Tokimeki论坛
{% endblock %}


{% block head %}
    <link rel="stylesheet" href="{{ static("front/css/index.css") }}"/>
{% endblock %}


{% block body %}
    <div class="lg-container">
        <div id="carousel-example-generic" class="carousel slide index-banner" data-ride="carousel">
            <!-- 指示器*小圆点 -->
            <ol class="carousel-indicators">
                <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
                <li data-target="#carousel-example-generic" data-slide-to="1"></li>
                <li data-target="#carousel-example-generic" data-slide-to="2"></li>
                <li data-target="#carousel-example-generic" data-slide-to="3"></li>
            </ol>

            <!-- 轮播图 -->
            <div class="carousel-inner" role="listbox">
                <div class="item active">
                    <a href="#">
                        <img src="https://static-image.xfz.cn/1529553938_445.png" alt="...">
                    </a>
                </div>
                <div class="item">
                    <a href="#">
                        <img src="https://static-image.xfz.cn/1533268381_580.jpg" alt="...">
                    </a>
                </div>
                <div class="item">
                    <a href="#">
                        <img src="https://static-image.xfz.cn/1532412054_279.png" alt="...">
                    </a>
                </div>
                <div class="item">
                    <a href="#">
                        <img src="https://static-image.xfz.cn/1529560399_230.jpg" alt="...">
                    </a>
                </div>
            </div>

            <!-- 左右切换的按钮 -->
            <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
                <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
                <span class="sr-only">Previous</span>
            </a>
            <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
                <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
                <span class="sr-only">Next</span>
            </a>
        </div>
    </div>
    <div class="sm-container">

    </div>
{% endblock %}
```

### 4.提示

一般都是自己重新写一个，不是去套用



