## 服务器

* 开启服务器

```
命令:python manage.py runserver ip:port
```

* 默认端口为8000
* 是纯python编写的轻量级web服务器，仅在开发阶段使用
* 服务器成功启动，提示信息:![](/assets/服务启动成功提示信息.png)

* 可以修改默认端口

```
python mangage.py runserver 8000
```

* 打开浏览器，输入网址:127.0.0.1:8000或者localhost:8000可以打开默认的页面
* 注意修改文件不需要重启服务器，如果增删文件需要重启服务器
* 通过ctrl+c停止服务器

---

## 管理操作

* 站点分为"内容发布"和"公共访问"
* "内容发布"的部分负责添加、修改、删除内容。django会根据定义的模型类自动生成管理模块

### 使用django的管理

* 创建管理员用户

```
python manage.py createsuperuser，按照提示输入用户名、邮箱、密码
```

* 启动服务器，通过'localhost:8000/admin"访问管理员管理界面，输入用户名密码完成登录
* 进入管理站点，默认可以对groups、users进行管理

### 管理界面本地化

* 编辑settings.py文件，设置编码与时区

```
例如设置为中国的时区和编码

LANGUAGE_CODE = 'zh-Hans'

TIME_ZONE = 'Asia/Shanghai'
```

### 向admin注册myapp的模型

* 打开myapp/admin.py 文件，注册模型

```
from django.contrib import admin
from .models import students,grades

# Register your models here.
admin.site.register(grades)
admin.site.register(students)
```

* 刷新管理页面

![](/assets/注册的模型.png)

* 可以对students和grades的数据进行增删查改操作
* 问题:如果在str方法中返回中文，在修改和添加时会包ascii的错误
* 解决:在str\(\)方法中，将字符串末尾添加".encode\('utf-8'\)"

---

#### 列表页属性

* list\_display:显示字段，可点击列头进行排序

```
class studentsAdmin(admin.ModelAdmin):
    list_display = ['pk','stu_name']

admin.site.register(students,studentsAdmin)
```

![](/assets/显示字段图.png)

* list\_filter:过滤字段，过滤框会出现在右侧

```
list_filter = ["stu_name"]
```

* search\_fields:搜索字段，搜索框会出现在上侧

```
search_fileds = ["stu_name"]
```

* list\_per\_page:分页，分页框会出现在下侧

```
list_per_page = 10
```

---

#### 添加、修改页属性

* fields:属性的先后顺序

```
fields= ['stu_name','stu_number']
```

* fieldsets:属性分组

```
fieldsets = [
     ('basic', {'fields': ['stu_name']}),
     ('more', {'fields': ['stu_number']}),
 ]
```

---

#### 关联对象

* 对于students模型类，有两种方式注册
  * 方式一:
    * 与grades模型类相同
  * 方式二:
    * 关联注册
* 按照grades的注册方式来注册students

```
1.
admin.site.register(students)


2.

from django.contrib import admin
from .models import students,grades

# Register your models here.

class studentsInline(admin.StackedInline):
    model = students
    extra = 2

class gradesAdmin(admin.ModelAdmin):
    inlines = [studentsInline]

admin.site.register(grades,gradesAdmin)
```

* 可以将内嵌的方式改为表格

```
class studentsInline(admin.TabularInline)
```

---

#### 布尔值的显示

* 发布性别的显示不是一个直观的结果，可以使用方法进行封装

```
def gender(sex):
    if sex.stu_sex:
        return '男'
    else:
        return '女'
gender.short_description = '性别'

在admin注册中使用gender代替stu_sex

class studentsAdmin(admin.ModelAdmin):

    list_display = ['stu_name','stu_grade',gender,'stu_date']
```



