前台视图

```
@bp.route('/')
def index():
    banners = BannerModel.query.order_by(BannerModel.priority.desc(),BannerModel.create_time.desc()).limit(4)
    context = {
        "banners":banners,
    }
    return render_template("front/index.html",**context)
```

轮播图动态获取数据

```
            <!-- 轮播图 -->
            <div class="carousel-inner" role="listbox">
                {% for banner in banners %}
                    {% if loop.first %}
                        <div class="item active">
                    {% else %}
                         <div class="item">
                    {% endif %}
                        <a href="{{ banner.link_url }}">
                            <img src="{{ banner.image_url }}" alt="...">
                        </a>
                    </div>
                {% endfor %}
            </div>
```



