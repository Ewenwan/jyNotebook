### 1.相关链接

模板网站:[http://www.17sucai.com/](http://www.17sucai.com/)

cms模板:[http://www.17sucai.com/search/cms后台模板?](http://www.17sucai.com/search/cms后台模板?)

### 2.定义宏

为了减少代码量，宏中的减号\(-\)是为了去掉转行

```
{% macro static(filename) -%}
    {{ url_for("static",filename=filename) }}
{%- endmacro %}
```



