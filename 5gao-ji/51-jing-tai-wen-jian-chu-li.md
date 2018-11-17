## 管理静态文件

* 项目中的css、图片、js都是静态文件

---

### 配置静态文件

* 在settings文件中定义静态内容

```
# 普通文件
STATICFILES_DIRS = [
    os.path.join(BASE_DIR,'static'),
]
```

* 在模板中可以使用编码

```
/static/myapp/image/1.jpg
```

* 在模板中可以使用static编码

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>miku</h1>
    <div>
         <img src="/static/myapp/image/1.jpg" width="100px" height="100px"/><br />
    </div>

    <div>
        {% load static from staticfiles %}
        <img src="{% static 'myapp/image/1.jpg' %}" width="100px" height="100px" alt="my image" />
    </div>

</body>
</html>
```



