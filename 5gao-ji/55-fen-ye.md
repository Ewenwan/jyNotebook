## 分页

* django提供了一些类实现管理数据分页，这些类位于django/core/paginator.py中

---

## Paginator对象

* Paginator\(列表,int\):返回分页对象，参数为列表数据，每面数据的条数

### 属性

* conut:对象总数
* num\_pages:页面总数
* page\_range:页码列表,从1开始,例如\[1,2,3,4\]

### 方法

* page\(num\):下标以1开始，如果提供的页码不存在，抛出InvalidPage异常

### 异常exception

* InvalidPage:当向page\(\)传入一个无效的页码时抛出
* PageNotAnInteger:当向page\(\)传入一个不是整数的值时抛出
* EmptyPage:当向page\(\)提供一个有效值，但是那个页面上没有任何对象时抛出

---

## Page对象

### 创建对象

* Paginator对象的page\(\)方法返回Page对象，不需要手动构造

### 属性

* object\_list:当前页上所有对象的列表
* number:当前页的序号，从1开始
* paginator:当前page对象相关的Paginator对象

### 方法

* has\_next\(\):如果有下一页返回True
* has\_previous\(\):如果有上一页返回True
* has\__other\_pages\(\):如果有上有一页或下一页返回True_
* next_\_page\_number\(\):返回上一页的页码，如果上一页不存在，抛出InvalidPage异常_
* len\(\):返回当前页面对象的个数
* 迭代页面对象:访问当前页面中的每个对象

---

## 示例

#### 创建视图studentpage

```
from .models import  Students,Grades
from django.core.paginator import  Paginator
def studentpage(request,pageid):

    if pageid == "":
        pageid = '1'
    # 所有学生列表
    stuList = Students.objects.filter(isDelete=False)
    # 划分为5个为一页
    pageNum = int(len(stuList)/5)
    # 第几份数据
    paginator = Paginator(stuList,pageNum)
    # 获取第pageid的数据
    page = paginator.page(pageid)
    print("pageid:",pageid)
    return render(request,'studentpage.html',{'students':page})
```

### 配置url

```
    # url(r'^studentpage/(\d+)/$', views.studentpage),
    re_path(r'studentpage/(?P<pageid>\d+)/$', views.studentpage),
```

### 定义模板studentpage.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ul>
        {% for stu in students %}
            <li>
                {{ stu.sname }} -- {{ stu.sgrade }}
            </li>
        {% endfor %}
    </ul>

    <ul style="">
        {% for index in students.paginator.page_range %}
            {% if index == students.number %}
                <li>
                {{ index }}
                </li>
            {% else %}
                <li>
                  <a href="/studentpage/{{index}}">{{index}}</a>
                </li>
            {% endif %}
        {% endfor %}
    </ul>
</body>
</html>
```





