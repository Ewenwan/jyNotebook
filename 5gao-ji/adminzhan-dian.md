### Admin站点

```
创建项目模板,默认Admin被启用:python manage.py startproject project醒目
创建管理员的用户名和密码:python manage.py createsuperuser
                       按照提示填写信息

在应用内admin.py文件完成注册,就可以在后台管理中维护模型的数据
from django.contrib import admin
from models import *

admin.site.register(Students)

查找admin文件:在INSTALLED_APPS项中加入django.contrib.admin,Django就会自动搜索每个应用的admin模块并将其导入
```

---

## ModelAdmin对象

* ModelAdmin类是模型在Admin界面中的表示形式
* 定义:定义一个类，继承于admin.ModelAdmin,注册模型时使用这个类

```
class StudentsAdmin(admin.ModelAdmin):

    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    # 设置页面列的名称
    gender.short_description = "性别"
    list_display = ['pk','sname','sage',gender,'scontend','sgrade','isDelete']
    list_per_page = 10
```

* 通常定义应用的admin.py文件里
* 使用方式一:注册参数

```
admin.site.register(Students,StudentsAdmin)
```

* 使用方式二:注册装饰器

```
from myapp.models import Students

@admin.register(Students)
class StudentsAdmin(admin.ModelAdmin):
```

* 通过重写admin.ModelAdmin的属性规定显示效果，属性主要分为列表页，增加修改页两部分

---

## 列表页选项

### “操作选项”的位置

* actions\__on\_top、actions\_on\_bottom:默认显示在页面的顶部_

```
    # 执行动作的位置
    # 在底部
    actions_on_bottom = True
    actions_on_top = True
```

### list\_display

* 出现列表中的显示字段
* 列表类型
* 在列表中，可以是字段名称，也可以是方法名称，但是方法名称默认不能排序
* 在方法中可以使用format\_html\(\)输出HTML内容

```
admin.py 

from django.contrib import admin

# Register your models here.
from .models import Grades,Students

# 注册

class StudentsInfo(admin.TabularInline):
    model = Students
    extra = 2

# class StudentsInfo(admin.StackedInline):
#     model = Students
#     extra = 2

@admin.register(Grades)
class GradesAdmin(admin.ModelAdmin):

    inlines = [StudentsInfo]

    # 列表页属性
    list_display = ['pk','gname','gdate','ggirlnum','gboynum','isDelete']
    list_filter = ['gname']
    search_fields = ['gname']
    list_per_page = 5

    # # 添加、修改页属性
    # fields = ['ggirlnum','gboynum','gname','gdate','isDelete']
    fieldsets = [
        ("num",{"fields":['ggirlnum','gboynum']}),
        ("base",{"fields":['gname','gdate','isDelete']}),
    ]

# admin.site.register(Grades,GradesAdmin)

@admin.register(Students)
class StudentAdmin(admin.ModelAdmin):

    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    # 设置页面列的名称
    gender.short_description = "性别"

    list_display = ['pk','sname','sage',gender,'scontend','sgrade','isDelete']
    list_per_page = 10

    # 执行动作的位置
    # 在底部
    actions_on_bottom = True
    actions_on_top = False

# admin.site.register(Students,StudentAdmin)

from .models import Text
admin.site.register(Text)



models.py

from django.db import models

# Create your models here.

# 班级》学生 ，一对多

# 类里面的属性，对应数据库中表的字段
class Grades(models.Model):

    gname    = models.CharField(max_length=20)
    gdate    = models.DateField()
    ggirlnum = models.IntegerField()
    gboynum  = models.IntegerField()
    isDelete = models.BooleanField(default=False)

    # 重写str
    def __str__(self):
        # return "%s-%d-%d" % (self.gname,self.ggirlnum,self.gboynum)
        return self.gname

class StudentsManager(models.Manager):
    def get_queryset(self):
        return super(StudentsManager,self).get_queryset().filter(isDelete=False)

    def createStudent(self,name,age,gender,contend,grade,isDel=False):
        stu = self.model()
        # print(type(stu))
        stu.sname = name
        stu.sage = age
        stu.sgender = gender
        stu.scontend = contend
        stu.sgrade = grade
        return stu

class Students(models.Model):

    # 定义一个类方法创建对象
    # cls代表了Students类
    @classmethod
    def createStudent(cls,name,age,gender,contend,grade,isDel=False):
        stu = cls(
            sname     = name,
            sage      = age,
            sgender   = gender,
            scontend  = contend,
            sgrade    = grade,
            isDelete  = isDel,
        )
        return stu

    # 自定义模型管理器
    # 当自定义模型管理器，objects就不存在了
    # stuObj = models.Manager()
    # stuObj2 = StudentsManager()

    sname = models.CharField(max_length=20)
    sgender = models.BooleanField(default=False)
    sage = models.IntegerField()
    scontend = models.CharField(max_length=20)
    isDelete = models.BooleanField(default=False)

    # 关联外键
    sgrade = models.ForeignKey("Grades",on_delete=models.CASCADE)

    def __str__(self):
        return self.sname

    def getName(self):
        return self.sname



# class TempTables(models.Model):
#     a = models.BooleanField(default=True)

from tinymce.models import HTMLField
class Text(models.Model):
    str = HTMLField()
```

* 让方法排序，为方法指定admin\__order\_filed属性:_

```
在models.py中为Students类增加方法orderName

    def orderName(self):
        return format(self.sname)

    orderName.admin_order_filed = 'sname'
```

* 标题栏名称:将字段封装成方法，为方法设置short\_description属性

```
@admin.register(Students)
class StudentsAdmin(admin.ModelAdmin):


    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    def getName(self):
        return self.sname

    getName.short_description = "姓名"
    list_display = ['pk', getName, 'sage', gender,]
```

### list\_filter

* 右侧栏过滤器，对那些属性的值进行过滤
* 列表类型
* 只能接受字段

```
@admin.register(Students)
class StudentsAdmin(admin.ModelAdmin):

    .....

    list_filter =  ('sname','sage')
```

### list\_per\_page

* 每页中显示多少项，默认设置为100

```
from django.contrib import admin

# Register your models here.
from myapp.models import Students, Grades


@admin.register(Students)
class StudentsAdmin(admin.ModelAdmin):

    .....

    list_per_page = 10
```

### search\_fileds

* 搜索框
* 列表类型，表示在这些字段上进行搜索
* 只能接收字段

```
class StudentsAdmin(admin.ModelAdmin):
    ...
    search_fields = ['sname']
```

* fieldsets:分组显示

```
class StudentsAdmin(admin.ModelAdmin):
    ...    
    fieldsets = (
        ('base',{'fields':('sname','sage')}),
        ('main',{'fields':('sgender','scontend')}),
    )
```

* fields与fieldsets两者选一

### 设置可点击链接进入编辑页面

```
list_display_links = ('sname','sage')
```

### 详细时间分层筛选

* date\_hierarchy

```
date_hierarchy = 'date'
```

---

### InlineModelAdmin对象

* 类型InlineModelAdmin:表示在模型的添加或修改页面嵌入关联模型的添加或修改
* 子类TabularInline:以表格的形式嵌入
* 子类StackedInline:以块的形式嵌入

```
class StudentsInline(admin.TabularInline):
    model = Students

class GradesAdmin(admin.ModelAdmin):
    inlines = [
        StudentsInline,
    ]
admin.site.register(Grades,GradesAdmin)
```

### 重写admin模板

* 在项目所在目录中创建templates目录，再创建一个admin目录
* 设置模板查找目录:修改settings.py的TEMPLATES项，加载模板时会在DIRS列表指定目录中搜索

```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

* 从django安装的目录下\(django/contrib/admin/templates\)将模板页面的源文件admin/base\_site.html拷贝到第一步创建好的目录中
* 编辑base\_site.html文件
* 刷新页面，查看效果
* 其他管理后台的模板可以按照相同的方式进行修改

```
base_site.html

{% extends 'admin/base.html' %}

{% block title %}
    {{ title }} |{{ site_title|default:_('Django site admin') }}
{% endblock %}

{% block branding %}
<h1 di="site-name"><a href="{% url 'admin:index' %}">学生管理系统</a></h1>
{% endblock %}

{% block nav-global %}
{% endblock %}
```



