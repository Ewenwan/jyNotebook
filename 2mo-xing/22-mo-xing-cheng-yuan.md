## 类的属性

* objects:是Manager类型的对象，用于数据库进行交互
* 当定义模型类时没有指定管理器，则Django会为模型类提供一个名为objects的管理器
* 支持明确指定模型类的管理器

```
class Grades(models.Model)
    grades = models.Manager()
```

* 当为模型类指定管理器后，django不再为模型类生成名为objects的默认管理器

---

## 管理器Manager

* 管理器是Django的模型进行数据库的查询操作的接口，Django应用的每个模型都拥有至少一个管理器
* 自定义管理器类主要用于两种情况
  * 情况一:向管理器类中添加额外的方法
  * 情况二:修改管理器返回的原始查询集:重写get\_queryset\(\)方法

```
class studentsManager(models.Manager):

    def get_queryset(self):
        return super(studentsManager,self).get_queryset().filter(isDelete=False)

class Students(models.Model):

    stuObj = studentsManager()
```

---

## 创建对象

* 当创建对象时，django不会对数据库进行读写操作
* 调用save\(\)方法才与数据库交互，将对象保存到数据库中
* 使用关键字参数构造对象很麻烦，推荐使用下面的两种方式
* 说明:\_\__init\_\_\_方法已经在基类models.Model中使用，在自定义模型中无法使用

* 方法一:在模型类中增加一个类方法:

```
class Students(models.Model):

    # 定义一个类方法创建对象
    # cls代表了students类
    @classmethod
    def createStudent(cls,name,age,gender,contend,grade,last,create,isDel=False):
        stu = cls(
            sname = name,
            sage = age,
            sgender = gender,
            scontend = contend,
            sgrade = grade,
            lastTime = last,
            createTime = create,
            isDelete = isDel
        )
        return stu

调用:book = Students.createStudent(name,age,...)
保存:book.save()
```

* 方法二:在定义管理器中添加一个方法
* 在管理器的方法中，可以通过self.model来得到它所属的模型类

```
class studentsManager(models.Manager):

    def get_queryset(self):
        return super(studentsManager,self).get_queryset().filter(isDelete=False)

    def createStudent(self,name,age,gender,contend,grade,last,create,isDel=False):
        stu = self.model()
        stu.sname = name
        stu.sage = age
        stu.sgender = gender
        stu.scontend = contend
        stu.sgrade = grade
        stu.lastTime = last
        stu.createTime = create
        stu.isDelete = isDel
        return stu

class Students(models.Model):

  ....

    stuObj = studentsManager()

调用:student = Students.stuObj.createStudent(name,age,...)
保存:student.save()
```

* 在方法二中，可以调用self.create\(\)创建并保存对象，不需要再手动save\(\)

```
class studentsManager(models.Manager):

    def get_queryset(self):
        return super(studentsManager,self).get_queryset().filter(isDelete=False)

    def createStudent(self,name,age,gender,contend,grade,last,create,isDel=False):
        stu = self.create(sname=name,sage=age,sgender=gender,scontend=contend,sgrade=grade,lastTime=last,createTime=create,isDelete=isDel)
        return stu

class Students(model.Model):
    ....
    stuObj = StudentsManager()


调用:student = Students.stuObj.createStudents(name,age,...)
查看:student.pk
```

---

## 实例属性

* DoesNotExist：在进行单个查询时，模型的对象不存在时会引发此异常，结合try/except使用

## 实例方法

* str\(self\):重写object方法，此方法在对象转换字符串时会被调用
* save\(\):将模型对象保存到数据表中
* delete\(\):将模型对象从数据表中删除



