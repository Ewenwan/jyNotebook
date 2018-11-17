### 1.安装

[安装地址](/1.kaifahuanjing/15-cun-chu-ku-de-an-zhuang/151-pymysqlde-an-zhuang.md)

### 2.连接数据库

在连接数据库之前，确保mysql已经打开了

```
import pymysql

# pymysql使用connect()方法连接数据库
db = pymysql.connect(host='127.0.0.1',user='root',password='123456',port=3306)
# 获取mysql的操作游标
cursor = db.cursor()
# 使用execute()方法执行sql语句
cursor.execute('select version()')
# 使用fetchone()方法来获得第一条数据
# fetchall()获取全部数据
data = cursor.fetchone()
print("database version:",data)
# 创建数据库并设置默认编码为utf-8
cursor.execute("create database spiders DEFAULT CHARACTER  set utf8")
db.close()
```

### 3.创建表结构

| 字段名 | 含义 | 类型 |
| :--- | :--- | :--- |
| name | 名字 | varchar |
| age | 年龄 | int |

```
import pymysql

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()
# 判断在数据库是否存在students表并创建name和age两个字段
# create table if not exists students(name varchar(255) not null,age int not null,primary key(name))
sql = 'create table if not exists students (name VARCHAR(255) not null,age int NOT NULL,PRIMARY KEY (NAME ))'
cursor.execute(sql)
db.close()
```

### 4.插入数据

```
mysql插入语句:insert into students(name,age) values('miku',18);
```

```
import pymysql

# 定义数据
name = 'miku'
age = 18

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()
sql = 'insert into students(name,age) VALUES (%s,%s)'
try:
    cursor.execute(sql,(name,age))
    # 提交
    db.commit()
except:
    # 回滚
    db.rollback()
db.close()
```

根据字典动态构造sql语句

```
import pymysql

data = {
    'name':'angle',
    'age':18,
}

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()

table = "students"
keys = ','.join(data.keys())
values = ','.join(["%s"] * len(data))
sql = "insert into {table}({keys}) VALUES ({values})".format(table=table,keys=keys,values=values)

try:
    if cursor.execute(sql,tuple(data.values())):
        print("成功")
        db.commit()
except:
    print("失败")
    db.rollback()
db.close()
```

### 5.更新数据

更新name字段值为angle的age字段，更改为235

```
import pymysql

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()

sql = "update students set age = %s where name = %s"
try:
    cursor.execute(sql,('235','angle'))
    db.commit()
except:
    db.rollback()
db.close()
```

根据字典动态构造sql更新语句

```
import pymysql

data = {
    "name":"angle",
    "age":18,
}
table = "students"
keys = ','.join(data.keys())
values = ','.join(["%s"]*len(data))

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()

# insert into students(name,age) VALUES (%s,%s) ON DUPLICATE KEY UPDATE name = %s, age = %s
# ON DUPLICATE KEY UPDATE:如果主键存在就执行更新操作
sql = "insert into {table}({keys}) VALUES ({values}) ON DUPLICATE KEY UPDATE".format(table=table,keys=keys,values=values)
update = ",".join([" {key} = %s".format(key=key) for key in data])
sql += update
print(sql)
try:
    if cursor.execute(sql,tuple(data.values())*2):
        print("成功")
        db.commit()
except:
    print("失败")
    db.rollback()
db.close()
```

### 6.删除数据

```
mysql语句:delete from table where 条件
```

```
import pymysql

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()

table = "students"
condition = "age = 18"
sql = "delete from {table} where {condition}".format(table=table,condition=condition)

try:
    cursor.execute(sql)
    db.commit()
except:
    db.rollback()
db.close()
```

### 7.查询数据

```
手动添加两条数据
mysql> insert into students values("angle",18);
Query OK, 1 row affected (0.06 sec)

mysql> insert into students values("miku",18);
Query OK, 1 row affected (0.09 sec)
```

```
import pymysql

db = pymysql.connect(host='localhost',user='root',password='123456',port=3306,db='spiders')
cursor = db.cursor()

table = "students"
condition = "age = 18"
sql = "select * from students where age = 18"

try:
    cursor.execute(sql)
    # 获取数据的数目
    print("count:",cursor.rowcount)
    # fetchone()方法获取第一条数据
    one = cursor.fetchone()
    print("one data:",one)
    # 调用fecthall()方法获取所有数据
    results = cursor.fetchall()
    print("results:",results)
    print("results type:",type(results))
    for row in results:
        print(row)
    db.commit()
except:
    print("error")
    # db.rollback()
db.close()
```

可以使用fetchone\(\)循环获取所有数据，注意fetchone\(\)方法，获取一条数据后，当前的第一条数据被取出来了就没有了，数据的指针会指向下一条数据

