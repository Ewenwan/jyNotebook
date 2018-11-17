抽离公共的内容

```
{% block head %} {% endblock %}
```

继承改写内容

```
{% extends 'cms/base.html' %}

{% block title %}
    个人信息
{% endblock %}
```



