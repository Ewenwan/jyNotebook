## ORM简介

* MVC框架中包括一个重要的部分，就是ORM，实现了数据模型与数据库的解耦，即数据模型的设计不需要依赖于特定的数据库，通过简单的配置就可以了轻松更换数据库
* ORM是"对象-关系-映射"的简称，主要的任务是:
  * 根据对象的类型生成表结构
  * 将对象、列表的操作，转换为sql语句
  * 将sql查询到的结果转换为对象、列表
* 极大地减轻了开发人员的工作量，不需要面对数据库变更而导致的无效劳动
* Django中的模型包含存储数据的字段和约束，对应着数据库中唯一的表

![](/assets/django模型.png)

---

## 使用mysql数据库

* 在python环境中安装mysql包

```
pip install pymysql
```

* 在mysql中创建数据库并设置编码为utf-8

```
create databases test charset=utf-8
```

* 打开settings.py文件，修改DATABASES项

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

---

## 开发流程

* 在models.py中定义模型类，要求继承自models.Model
* 把应用加入settings.py文件的installed\_app项
* 生成迁移文件
* 执行迁移生成表
* 使用模型类进行crud操作

---

## 使用数据库生成模型类

django根据现有数据库建立model，引入外部数据库

```
python manage.py inspectdb > myapp/models.py
```



