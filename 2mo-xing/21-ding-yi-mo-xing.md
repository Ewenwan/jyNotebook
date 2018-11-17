## 定义模型

* 在模型中定义属性，会生成表中的字段
* django根据属性的类型确定一下信息:
  * 当前选择的数据库支持字段的类型
  * 渲染管理表单时使用的默认html控件
  * 在管理站点最低限度的验证
* django会为表增加自动增长的主键列，每个模型只能由一个主键列，如果使用选项设置某属性为主键列后，则django不会再生成默认的主键列
* 属性命名限制
  * 不能是python的保留关键字
  * 由于django的查询方式，不允许使用连续的下划线

---

## 定义属性

* 定义属性时，需要字段类型
* 字段类型被定义在django.db.models.fileds目录下,为了方便使用，被导入到django.db.models中
* 使用方式
  * 导入from.django.db import models
  * 通过models.Field创建字段类型的兑现，赋值给属性
* 对于重要数据都做逻辑删除，不做物理删除，实现方法是定义isDelete属性，类型为BooleanField，默认值为False

---

## 字段类型

* AutoField:一个根据实际ID自动增长的InteGErField,通常不指定。如果不指定，一个主键字段将自动添加到模型中
* BooleanField；true/false字段，此字段的默认表单控制是CheckboxInput
* NullBooleanField:支持null，false，true三种值
* CharField\(max\_length=字符长度\):字符串，默认的表单样式是TextInput
* TextField:大文本字段，一般超过400使用，默认的表单控件是Textarea
* IntegerFeild:整数
* DecimalFeild\(max_digits=None,decimal\_places=None_\):使用python的decimal实例表示的十进制浮点数
  * DecimalField.max\_digits:位数总数
  * DecimalField.decimal\_places:小数点后的数字位数
* FloatField:用python的float实例来表示的浮点数
* DateField\[auto_now=False,auto\_now\_add=False_\]:使用python的datetime.date实例表示的日期
  * 参数DateFiled.auto\_now:每次保存对象时，自动设置该字段为当前时间，用于"最后一次修改"的时间戳，总是使用当前日期，默认为false
  * 参数DateFiled.auto\_now\_add:当对象第一次被创建时自动设置当前时间，用于创建的时间戳，总是使用当前日期，默认为false
  * 该字段默认对应的表单控件是一个TextInput，在管理员站点添加了一个JavaScript写的日历控件，和一个"Today"的快捷按钮，包含了一个额外的invalid\_date错误消息建
  * auto-\_now-\_add,auto\_now,and default 这些设置是相互排斥的，它们之间的任何组合将会发生错误
* TimeFiled:使用python的datetime.time实例表示的时间，参数同DateField
* DateTimeFiled:使用python的datetime.datetime实例表示的日期和时间,参数同DateField
* FileField:一个上传文件的字段
* ImageField:继承了FileField的所有属性和方法，但对上传的对象进行校验，确保是个有效的image

---

## 字段选项

* 通过字段选项，可以实现对字段的约束
* 在字段对象时通过关键字参数指定
* null:如果为True，Django将空值以NULL存储到数据库中，默认值是False
* blank:如果为True，则该字段允许为空白，默认值是False
* 对比:null是数据库范畴的概念，blank是表单验证证范畴的
* db\_column:字段的名称，如果未指定，则使用属性的名称
* db\_index:若值为True，则在表中会为此字段创建索引
* default:默认值
* primary\_key:若为True，则该字段会成为模型的主键字段
* unique:如果为True，这个字段在表中必须有唯一值

---

## 关系

* 关系的类型包括
  * Foreignkey:一对多，将字段定义在多的端中
  * ManyToManyField:多对多，将字段定义在两端中
  * OneToOneField:一对一，将字段定义在任意一端中
* 可以维护递归的关联关系，使用"self"指定，详见"自关联"
* 用一访问多:对象.模型类小写\_set

```
gradesinfo.studentsinfo_set
```

* 用一访问一:对象.模型类小写

```
studentsinfo.gradesinfo
```

* 访问id:对象.属性\_id

```
grades.students_id
```

---

## 元选项

* 在模型类中定义类Meta，用于设置元信息
* 元信息db\_table:定义数据表名称，推荐使用小写字母，数据表的默认名称

```
<app_name>_<model_name>
```

* ordering:对象的默认排序字段，获取对象的列表时使用，接收属性构成的列表
* 字符串前加-表述倒序，不加-表示正序
* 注意:排序会增加数据库的开销

```
class Grades(model.Model)

    class Meta():
        ordering = ['id']
        ordering = ['-id']
```

---

# 示例演示

* 创建test2项目，并创建myapp应用，使用mysql数据库
* 定义班级模型

```
class gradesInfo(models.Model):

    class Meta():
        ordering = ['name']

    name = models.CharField(max_length=20)
    number = models.IntegerField()
    isDelete = models.BooleanField(default=True)
```

* 定义学生模型

```
class studentsInfo(models.Model):

    class Meta():
        ordering = ['name']

    name = models.CharField(max_length=20)
    age = models.IntegerField()
    date = models.DateTimeField()
    grade = models.ForeignKey('gradesInfo',on_delete=models.CASCADE)
```

```
1.django-admin startproject project
2.python manage.py startapp myapp
3.python manage.py makemigrations
4.python manage.py migrate
5.python manage.py runserver
6.创建数据库create database angle default charset utf8 collate utf8_general_ci;


配置数据库:
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'miku2',
        'USER': 'root',
        'PASSWORD': '123456',
        'PORT':3306,
    }
}


修改地区和时区
LANGUAGE_CODE = 'zh-Hans'

TIME_ZONE = 'Asia/Shanghai'


安装mysql配置
import pymysql

pymysql.install_as_MySQLdb()
```

* 定义students、grades视图

```
from django.shortcuts import render
from django.http import HttpResponse
from .models import Grades,Students

# 学生信息
def students(request):
    studentsList = Students.objects.all()
    return render(request, 'myapp/students.html',{"students":studentsList})

# 班级信息
def grades(request):
    gradesList = Grades.objects.all()
    return render(request,'myapp/grades.html',{'grades':gradesList})
```

* students.html、grades.html模板

```
students.html

"""
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>学生信息</title>
</head>
<body>
    <h1>学生信息列表</h1>
    <ul>
        {% for student in students %}
            <li>
            {{ student.pk }} -- {{ student.sname }} -- {{ student.sgrade }}
            </li>
        {% endfor %}
    </ul>
</body>
</html>
"""


grades.html

"""
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>班级表</title>
</head>
<body>
    <h1>班级信息</h1>
    <ul>
        {% for grade in grades %}

            <li>
                {{ grade.pk }} -- {{ grade.gname }}
            </li>
            {% for student in grade.students_set.all %}
                <li>学生:{{ student.sname}}</li>
            {% endfor %}
        {% endfor %}
    </ul>
</body>
</html>
"""
```

* 配置url，能够完成班级及学生的展示

```
配置路由；

from django.conf.urls import url,include
from . import views

urlpatterns = [
    url(r'^students/$',views.students),
    url(r'^grades/$',views.grades),
]

展示省略---
```

## 测试数据

* grades的测试数据

```
insert into myapp_grades(gname,gdate,ggirlnum,gboynum,isDelete) values
("python01","2017-2-4",10,50,0),
("python02","2017-3-6",4,34,0),
("python03","2017-4-16",12,60,0),
("python04","2017-5-4",3,75,0);
```

* students的测试数据

```
insert into myapp_students(sname,sgender,scontend,isDelete,sgrade_id,sage)
("miku1",1,"I am miku1",0,1,25),
("miku2",1,"I am miku2",0,2,32),
("miku3",0,"I am miku3",0,1,12),
("miku4",1,"I am miku4",0,2,45),
("miku5",0,"I am miku5",0,3,7),
("miku6",1,"I am miku6",0,4,10),
("miku7",0,"I am miku7",0,2,11),
("miku8",1,"I am miku8",0,3,15),
("miku9",1,"miku9",0,1,16),
("miku10",0,"I am miku10",0,2,18),
("miku11",1,"I am miku11",0,3,18),
```



