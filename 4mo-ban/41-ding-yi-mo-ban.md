## 定义模板

* 模板语言包括
* 变量
* 标签{百分号 代码块 百分号}
* 过滤器
* 注释{\#代码或HTML\#}

---

### 变量

* 语法

```
{{variable}}
```

* 当模板引擎要一个变量，将计算这个变量，然后将结果输出

* 变量名必须由字母、数字、下划线\(不能以下划线开头\)和点组成

* 当模板引擎遇到点\("."\)，会按照下列顺序查询:

  * 1.字典查询,例如:key\['value'\]
  * 2.属性或方法查询:例如key.value
  * 3.数字索引查询，例如:key\[value\]

* 如果变量不存在，模板系统将插入\(空字符串\)""

* 在模板中调用方法时不能传递参数

---

### 在模板中调用对象的方法

* 在models.py中定义类Grades

```
from django.db import models

# Create your models here.

class GradesManager(models.Manager):

    def get_queryset(self):
        return super(GradesManager,self).get_queryset().filter(isDelete=False)

    def createGrades(self,name,date,gril,boy,isDel):
        g = self.model()
        g.gname = name
        g.gdate = date
        g.ggrilnum = gril
        g.gboynum = boy
        g.isDelete = isDel
        return g

class Grades(models.Model):

    gObj = GradesManager()

    gname    = models.CharField(max_length=20)
    gdate    = models.DateField()
    ggirlnum = models.IntegerField()
    gboynum  = models.IntegerField()
    isDelete = models.BooleanField(default=False)
```

* 在views.py中传递Grades对象

```
from django.shortcuts import render
from django.shortcuts import  *

# Create your views here.

def index(request):
    context = {'hello':'hello world'}
    return render(request,'myapp/index.html',context)
```

* 在模板index.html中调用

```
{{ hello }}
```

---

### 标签

* 语法:{百分号tag百分号}
* 作用

  * 在输出中创建文本
  * 控制循环或逻辑
  * 加载外部信息到模板中供以后的变量使用

* for标签

```
{%for ... in ...%}

循环逻辑

{{forloop.counter}}标识当前是第几次循环

{%empty%}

给出的列表为列表不存在时，执行此处

{%endfor%}
```

* if标签

```
{%if ...%}

逻辑

{%elif ...%}

逻辑

{%else%}

逻辑

{%endif%}
```

* comment标签

```
{% comment %}

多行注释

{% endcomment %}
```

* include:加载模板并以标签内的参数渲染

```
{%include "myapp/footer.html" %}
```

* url:反向解析

```
{% url 'app:name' p1 p2%}
```

* crst\_token:这个标签用于跨站请求伪造保护

```
{%crsf_token%}
```

* 布尔标签:and、or、and比or的优先级高
* block、extends:详见"继承模板"
* autoescape:详见"HTML"转义

---

### 过滤器

* 语法:,例如，表示将变量name的值变为小写输出
* 使用管道符号\\(\\|\\)来应用过滤器
* 通过使用过滤器来改变变量的计算结果
* 可以在if标签中过滤器结合运算符

```
if list|length > 1
```

* 过滤器能够被"串联",构成过滤器链

```
name|lower|upper
```

* 过滤器可以传递参数，参数使用引号包起来

```
list:join:","
```

* default:如果一个变量没有被提供，或者为fals额或空，则使用默认值，否则使用变量的值

```
value|default:"没有初始化"
```

* date:根据给定格式一个date变量格式化

```
value|date:"Y-m-d"
```

* escape:详见"HTML转义"
* 详细的过滤器
* value\|add:number

```
<h1>
num = {{num}}
</h1>
<h1>
num = {{num|add:10}}
</h1>
<h1>
num = {{num|add:-5}}
</h1>
```

* -- 乘法
* num/1\*5

```
  # num={%widthratio num 1 5%}

  # num={%widthratio num 5 1%}
```

---

### 注释

* 单行注释

```
{#....#}
```

* 注释可以包含任何模板代码，有效的或者无效的都可以

```
{{#{% if a %}bar{%else%}#}
```

* 示例:查询所有班级，要求奇数行显示红色，偶数行显示为蓝色

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>
Title
</title>
</head>
<body>
<ul>
{#        {{ grades }}#}

       {% for grade in grades%}
          {% if forloop.counter|divisibleby:2  %}

<li style="background-color: green">

               {% else %}

<li style="background-color: pink">

           {% endif %}
            {{ grade.gname }} -- {{ grade.gdate }}
            {%empty%}
             目前没有信息

</li>

       {% endfor %}

</ul>
</body>
</html>
```

额外知识点

```
forloop.counter    索引从 1 开始算
forloop.counter0    索引从 0 开始算
forloop.revcounter    索引从最大长度到 1
forloop.revcounter0    索引从最大长度到 0
forloop.first    当遍历的元素为第一项时为真
forloop.last    当遍历的元素为最后一项时为真
forloop.parentloop 用在嵌套的 for 循环中，获取上一层for 循环的 forloop
```



