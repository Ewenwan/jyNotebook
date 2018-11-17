# 44 url\_for反转蓝图注意事项

* 如果使用蓝图，那么以后想要反转蓝图中的视图函数为url，那么就应该在使用url\_for的时候就指定这个蓝图。比如news.news\_list，否则就找不到这个endpoint，在模板中的url\_for同样也是满足这个条件，就是指定蓝图的名字
* 即使在同一蓝图中反转视图函数，也要指定蓝图的名字

```text
app.py

@app.route('/')
def hello_world():
    # url_for('指定蓝图名字.视图函数名字')
    print(url_for('news.news_list'))
    return render_template('index.html')

------------------------------------------------

index.html

<a href="{{ url_for('news.news_list') }}">点击</a>
```

![](../.gitbook/assets/44-1.png)

