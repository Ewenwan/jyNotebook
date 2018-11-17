## 设计介绍

* ###### 学生表结构设计

  * ###### 表名:students
  * ###### 学生名:stu\_name
  * ###### 学生班级:stu\_grade
  * ###### 学生性别:stu\_sex
* ###### 班级表结构设计

  * ###### 表名:grades
  * ###### 班级名:gra\_name
  * ###### 班级人数:gra\_number

---

## 数据库配置

* 在settings.py文件中，通过DATABASES项进行数据的配置
* 配置mysql数据库

```
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    # }
    'default':{
        'ENGINE':'django.db.backends.mysql',
        'NAME':'miku',
        'USER':'root',
        'PASSWORD':'123456',
        'PORT':3306,
    }
}
```

* 解释:
  * 'ENGINE':选择数据库，可为 'django.db.backends.postgresql\_psycopg2', 'django.db.backends.mysql', 'django.db.backends.sqlite3', 'django.db.backends.oracle'
  * NAME':实际mysql1的database的名字，并不是数据库的名字
  * ‘USER’:'root',\#mysql数据库用户名
  * 'PASSWORD':用户对应的密码
  * 'HOST':数据库主机地址
  * 'POST':数据库端口，默认端口为3306
* 在控制平台中输入mysql -u root -p
* 输入密码:123456
* 创建与之对应的数据库名miku

---

## 创建应用

* 创建应用命令

```
python manage.py startapp myapp
```

* 应用的目录结构图

![](/assets/应用目录结构图.png)

---

## 定义模型类

* 一个数据表对应一个类
* 在models.py文件中，定义模型类
* 引入包名from django.db import models
* 模型类继承自models.Model类
* 当输出兑现时；会调用对象的str方法

_tips:不需要定义主键列，在生成的时候自动添加，并且值为自动增长_

```
# model.py

from django.db import models

# Create your models here.
class grades(models.Model):
    gra_name = models.CharField(max_length=20)
    gra_number = models.IntegerField()

    def __str__(self):
        return "第%d个 | %s班 | 共有%d人数" % (self.pk,self.gra_name,self.gra_number)

class students(models.Model):
    stu_name = models.CharField(max_length=20)
    stu_grade = models.ForeignKey("grades",on_delete=models.CASCADE)
    stu_sex = models.BooleanField()
    stu_date = models.DateTimeField()

    def __str__(self):
        return "第%d个 | 姓名:%s | %s班 | 性别:%d |日期:%s" % \
               (self.pk, self.stu_name, self.stu_grade,self.stu_sex,self.stu_date)
```

---

## 生成数据表

* 激活模型:编辑settings.py文件，将myapp应用加入到installed\_apps中
* ```
  # Application definition

  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'myapp',
  ]
  ```
* 生成迁移文件:根据模型类生成sql语句

```
python manage.py makemigrations
```

```
django.core.exceptions.ImproperlyConfigured: Error loading MySQLdb module.
Did you install mysqlclient?

如果遇到这样的错误
需要安装pymysql模块
命令安装:pip install pymysql

然后再django项目的__init__下设置:

import pymysql
pymysql.install_as_MySQLdb()
```

```
TypeError: __init__() missing 1 required positional argument: 'on_delete'

错误代码:
stu_grade = models.ForeignKey("grades")

修改后:
stu_grade = models.ForeignKey("grades",on_delete=models.CASCADE)
```

```
django.db.utils.OperationalError: (1045, "Access denied for user 'root'@'localhost' 
(using password: NO)")
这是由于用的mysql版本太新了，换成5.7版本的
mysql下载地址:https://dev.mysql.com/downloads/file/?id=478035
```

![](/assets/生成迁移文件.png)

* 执行迁移:执行sql语句生成数据表

```
python manage.py migrate
```

![](/assets/执行迁移.png)

---

## 测试数据操作

* 进入python shell，进行简单的模型api练习

```
python manage.py shell
```

* 进入shell后提示如下:

![](/assets/测试shell.png)

* 引入需要的包:

```
In [1]: from myapp.models import grades,students

In [2]: from django.utils import timezone

In [3]: from datetime import *
```

* 查询所有班级信息

```
In [4]: grades.objects.all()
Out[4]: <QuerySet []>
```

* 新建班级信息

```
In [5]: a = grades()

In [6]: a.gra_name="1"

In [7]: a.gra_number=2

In [8]: a.save()

In [9]: a
Out[9]: <grades: 2>
```

* 查找班级信息

```
In [4]: grades.objects.get(pk=1)
Out[4]: <grades: 第1个 | 班 | 共有25人数>

In [5]: grades.objects.get(pk=2)
Out[5]: <grades: 第2个 | 1班 | 共有2人数>

In [6]: a = grades.objects.get(pk=2)

In [7]: a
Out[7]: <grades: 第2个 | 1班 | 共有2人数>
```

* 修改班级信息

```
In [9]: a = grades.objects.get(pk=1)

In [10]: a.gra_name = "2"

In [11]: a
Out[11]: <grades: 第1个 | 2班 | 共有25人数>
```

* 删除班级信息

```
In [16]: a.delete()
Out[16]: (1, {'myapp.students': 0, 'myapp.grades': 1})
```

---

## 关联对象的操作

* 对于students表可以按照以上操作方式进行
* 添加、注意添加关联对象

```
In [34]: a = grades.objects.get(pk=2)

In [35]: a
Out[35]: <grades: 第2个 | 2班 | 共有26人数>

In [36]: b = students()

In [37]: b.stu_name = "miku"

In [38]: b.stu_grade = a

In [39]: b.stu_sex = 1

In [40]: b.stu_date = datetime(year=2017,month=10,day=26)

In [41]: b.save()
E:\Python36\lib\site-packages\django\db\models\fields\__init__.py:1423: RuntimeWarning: DateTimeField students.stu_date received a naive datetime (2017-10-26 00:00:00) while time zone support is active.
  RuntimeWarning)

In [42]: b
Out[42]: <students: 第1个 | 姓名:miku | 第2个 | 2班 | 共有26人数班 | 性别:1 |日期:2017-10-26 00:00:00>
```

![](/assets/关联对象student.png)

* 获得关联集合:返回当前grades对象的所有students对象

grades对象.students对象名\_set.all\(\)

```
In [43]: a.students_set.all()
Out[43]: <QuerySet [<students: 第1个 | 姓名:miku | 第2个 | 2班 | 共有26人数班 | 性别:1 |日期:2017-10-26 00:00:00+00:00>]>
```

* 有一个students存在，必须要有一个grades对象，提供了创建关联的数据

a.students.\_set.create\(\)

```
In [44]: b = a.students_set.create(stu_name="miku",stu_sex=False,stu_date=datetime(year=2016,month=5,day=26)
    ...: )
E:\Python36\lib\site-packages\django\db\models\fields\__init__.py:1423: RuntimeWarning: DateTimeField students.stu_date received a naive datetime (2016-05-26 00:00:00) while time zone support is active.
  RuntimeWarning)

In [45]: b
Out[45]: <students: 第2个 | 姓名:miku | 第2个 | 2班 | 共有26人数班 | 性别:0 |日期:2016-05-26 00:00:00>
```



