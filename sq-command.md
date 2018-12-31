### 准确型数据类型

| sql server数据类型 | 说明 |
| :--- | :--- |
| bigint | 8字节 |
| int | 4字节 |
| smallint | 2字节 |
| tinyint | 存储从0到255之间的整数 |
| bit | 存储0或1 |
| numeric\(p,q\)或decimal\(p,q\) | 定点精度和小数位数 |

---

### 近似型数据类型

| sql server数据类型 | 说明 |
| :--- | :--- |
| float | 8字节 |
| real | 4字节 |

---

### 字符串类型

| sql server数据类型 | 说明 |
| :--- | :--- |
| char\(n\) | 定长字符串类型 |
| varchar\(n\) | 可变长字符串类型 |
| text | 文本 |
| nchar\(n\) | 统一字符编码，定长字符串类型 |
| nvarchar\(n\) | 可变长字符串类型 |
| ntext | 统一字符编码文本 |
| binary\(n\) | 定长二进制字符数据 |
| varbinary\(n\) | 可变长二进制字符数据 |
| image | 大容量、可变长二进制字符数据，存储格式为word，excel，bmp，gif，jpeg..... |

---

### 日期时间类型

| sql server数据类型 | 说明 |
| :--- | :--- |
| datetime | 8字节，精确到百分之三秒\(3.33毫秒\) |
| smalldatetime | 4字节，精确到分钟 |

---

* '建表'

```
create table 表名(
    列名>数据类型 [列级完整性约束定义],
    ...,
    [,表级完整性约束定义])

列级完整性约束:
    NOT NULL:限制列取值为空
    DEFAULT:指定列的默认值
    UNIQUE:限制列的取值范围
    CHECK:限制列的取值范围
    PRIMARY KEY:指定本列为主码


定义主码约束:
    列级
    <列名> 数据类型 PRIMARY KEY [(<列名>[,...n])]
    表级
    PRIMATY KEY (<列名>[,...n])


定义外码约束:
    [FOREIGN KEY (<列名>)] REFERENCES <外表名>(<外表列名>)
    [on delete {cascade | on action}]
    [on update {caseade | on action}]

    on delete cascade:级联删除。表示当删除主表中的记录时，如果在子表中有对这些记录的主码值的引用，则一起删除这些记录
    on delete on action:限制删除。表示当删除主表中的记录时，如果在子表中有对这些记录的主码值的引用，则拒绝删除主表中的记录
    on update cascade:级联更新。表示当上删除主表中的有子表引用的列值时，如果在子表中有对这个列值的引用，则一起更改
    on update no action:限制更新，拒绝更新
```

* '删除表'

```
drop table 表名,[....]
```

* '修改表'

```
alter table 表名
    alter column <列名>新数据类型   -- 修改列定义
    add <列名>数据类型约束定义       -- 添加新列
    drop column <列名>             -- 删除列
    add [constraint <约束名> 约束定义]  -- 添加约束
    drop [constraint <约束名>]        -- 删除约束



'修改表 - 主码约束'
alter table 表名
    add [constraint <约束名>]
    primary key (<列名>[,...n])

'修改表 - UNIQUE约束'
alter table 表名
    add [constraint <约束名>]
    unique (<列名> [,....n])

'修改表 - 外码约束'
alter table 表名
    add [constraint <约束名>]
    foreign key (<列名>) REFERENCES 引用表名 (<列名>)

'修改表 - DEFAULT约束'
alter table 表名
    add constraint <约束名>
    default 默认值 for 列名
```

---

### 数据操作语句

```
select 列名(字段) from 表名 (where = 行选择条件)
group by 分组依据列(列名)
having 组选择条件
order by 排序依据列

'检索前n列'
select top n 列名 form表名

'不重复'
select distinct 列名 from 表名;
```

查询条件

| 查询条件 | 谓词 |
| :--- | :--- |
| 比较 | =、&gt;、&gt;=、&lt;、&lt;=、&lt;&gt;\(或!=\)以及NOT+前述比较运算符 |
| 确定范围 | between and、not between and |
| 确定集合 | in、not in |
| 字符匹配 | like、not like |
| 空值 | is null、is not null |
| 多重条件 | and、or |

```
注意:
like运算符，通配符含义
_(下划线):匹配任意一个字符
%(百分号):匹配至少0个字符
[]:匹配[]中的任意一个字符

rtrim:去掉指定列中的尾随的空格


ESCAPE转义字符
'将！作为转义字符'
where name like '%123!%%' escape '!'



聚合函数
count(*):统计表中元组个数
count([distinct] <列名>):统计本列非空列值个数,distinct 表示不重复列
sum:总和
avg:计算平均值
max:最大值
min:最小值
```

* 分页操作 \*\*\*

  SELECT \* FROM table LIMIT \[offset,\] rows \| `rows OFFSET offset`   
    \(LIMIT offset, `length`\)

```
例如:
select * from table limit 0,10;//检索第1行-10行

select * from table limie 5,-1;//检索第6行至最后
```

---

### 多表连接查询

```
from 表1 [as] <别名> [inner] join 表2 on <连接条件>
from 表1 left|right [outer] join 表2 on <连接条件>
```

---

```
使用top限制结果集
top n [percent] [with ties]
n:非负整数
top n:表示去前n行数据
top n percent:表示去查询结果的前n%行数据
with ties:表示包括并列的结果


查:select 列名 form 表名 (where = 条件)
删除:delete form 表名 (where = 条件)
增:insert [into] <表名> [{<列表名>}] values (值列表)
更:update <表名> set <列名> = 表达式...
```

---

### 建立索引

```
create [unique] [clustered | nonclustered] index 索引名 on 表名 (列名)

unique:唯一索引
clustered:聚焦索引
nonclustered:非聚集索引

drop index <索引名>
```

---

### 定义视图

```
建立视图:create view <视图名> [(列名 [,...n])] as 查询语句
修改视图:alter view 视图名 [(列名[,...n])] as 查询语句
删除视图:drop view <视图名>
```

---

```
利用T-SQL语句创建数据库
'数据库'
CREATE DATABASE 数据库名
ON
(
    NAME = 数据库名, # 指定文件的逻辑名称
    FILENAME = 'path\数据库名.mdf',
    SIEX=10,
    # 指定文件可增大到的最大大小
    # 指定文件大小无限制
    MAXSIZE = 30,
    FILEGROWTH = 5# 指定文件的自动增量
)
'日志'
LOG ON 
(
 NAME = '数据库名_log',
 FILENAME = 'PATH\数据库名_log.ldf'，
 SIZE = 3,
 MAXSIZE = 12,
 FILEGROWTH = 2   
)

'删除数据库'
drop database 数据库名
```

---

## 变量

```
-- 声明局部变量
-- DECLARE @局部变量名 [as] 数据类型
DECLARE @x int,@y int,@z int
-- 赋值
-- set @变量名=值
SET @x=10
SET @y=10
SET @z=@x+@y
Print @z
```

---

## 流程控制语句

| 语句 | 描述 |
| :--- | :--- |
| BEGIN...END | 定义语句块 |
| BREAK | 退出最内层的WHILE循环 |
| CONTINUE | 重新开始WHILE循环 |
| GOTO标签 | 从"标签"所定义的标签之后的语句处继续进行处理 |
| IF...ELSE | 如果指定条件为真，执行一个分支，否则执行另一个分支 |
| RETURN | 无条件退出 |
| WHILE | 当指定条件为真时重复一些语句 |

```
-- BEGIN .. END语句
DECLARE @i int,@sum int
set @i=1
set @sum=0
WHILE @i <= 100
BEGIN
    SET @sum = @sum+@i
    SET @i = @i+1
END
Print @sum

-- if .. else
if @sum = 5050
    Print 1
else
    Print 0
```

---

## 存储过程

### 创建和执行存储过程

创建存储过程的sql语句为create procedure,其语法格式为:

```
create proc[edure] 存储过程名
[ {@参数名 数据类型 } [=default ] [output]  ][,...n]
as
    SQL语句 [,...n]
```

* default:表示参数的默认值。如果定义了默认值，则在执行存储过程中，可以不必指定该参数的值
* OUTPUT:表明参数是输出参数。该选项的值可以返回给EXEC\[UTE\]。使用OUTPUT参数可将信息返回给调用者

```
---- 创建存储过程
----create proc [edure] 存储过程名
----[{@参数名 数据类型} [=default] [output]][,...n]
----AS
----    SQL语句[..n]
---- defualt:表示默认值
---- output:表名参数是输出参数。该选项的值可以返回给EXEC{UTE}

-- 建立存储
--create procedure p_grade1
--as 
--    select sname,cname,grade
--    from student s inner join sc
--    on s.sno = sc.sno inner join course c
--    on c.cno = sc.cno
--    where sdept = '计算机系'

--go
-- 执行存储过程
--EXEC p_grade1

---- 建立含有参数的存储过程
--create procedure p_grade3
--    @dept char(20) 
--as 
--    select sname,cname,grade
--    from student s inner join sc
--    on s.sno = sc.sno inner join course c
--    on c.cno = sc.cno
--    where sdept = @dept

-- 含有多个参数并有默认值的存储过程
--create procedure p_grade4
--@student_name char(10),@course_name char(20) = '数据库基础'
--as
--select sname,cname,grade
--from student s inner join sc
--on s.sno = sc.sno inner join course c
--on c.cno = sc.cno
--where sname = @student_name
----and cname = @course_name

----exec p_grade4 '刘晨','VB'

-- 含多个输入参数并均指定默认值的存储过程
--create procedure P_Student
--@dept char(20) = '计算机系',@sex char(2) = '男',@age int = 20
--as
--    select * from student
--    where sdept = @dept
--    and Ssex = @sex
--    and sage = @age

---- 执行存储过程
--EXEC P_Student

---- 含有输出的存储过程
--create procedure p_sum
--@var1 int,@var2 int,@var3 int output
--as 
--set @var3 = @var1 * @var2

--go

--declare @res int
--execute p_sum 5,7,@res output
--print @res

--go

-- alter proc [edure]存储过程名 ....
-- drop {proc|procedure} {procedure}[..n]
```

---

## 触发器

### 创建触发器

建立触发器T-SQL语句为:CREATE TRIGGER,其语法格式为:

```
create trigger 触发器名称
on {表名|视图名}
{FOR | AFTER | INSTEAD OF}
{ [INSERT ][,] [DELETE][,][UPDATE]}
AS
    SQL语句
```

* 触发器名称在数据库中必须是唯一的
* ON子句用于指定在其上执行触发器的表名或者是视图名
* AFTER:指定触发器只有引发触发器执行的SQL语句都已成功执行后，才执行此触发器
* FOR:作用同AFTER
* INSTEAD OF:指定执行触发器而不是执行触发器执行的SQL语句，从而代替触发语句的操作
* INSERT、DELETE和UPDATE是引发触发器执行的操作，若同时指定多个操作，则各操作之间用逗号分隔
* INSERTED表保存了INSERT操作中新插入的数据和UPDATE操作中更新后的数据
* DELETED保存了DELETE操作删除的数据和UPDATE操作中更新前的数据

---

## 后触发型触发器

使用FOR或AFTER选项定义的触发器为后触发型的触发器，即只有在引发触发器执行的语句中指定的操作都已成功执行，并且所有的约束检查也成功完成后，才执行触发器

注意:不能在视图上定义AFTER触发器

```
限制职工表中的"浮动工资"列的取值必须在"基本工资"的(0~30)%范围内

create trigger tri_floatpay
on 职工表 after insert,update
as
    if exists(select * from inserted where 浮动工资 not betwwen 0 and 基本工资 * 0.31)
        rollback -- 撤销操作

rollback实际是将数据库回滚到引发触发器的操作之前的状态，也就是撤销了违反完整性约束的操作
```

## 前触发型触发器

使用INSTEAD OF选项定义的触发器为前触发型触发器。

* 在表或视图上，每个INSERT、UPDATE或DELETE操作最多只可定义一个INSTEAD OF 触发器

```
create trigger tri_salary
on 职工表 instead of insert
as 
    if not exists(select * from 职工表 a join 工作表 b on a.工作号 = b.工作号 where 基本工资 not between 最低工资 and 最高工资)
        insert into 职工表 select * from inserted -- 重做操作

    当前触发型触发器执行时，引发触发器执行的数据操作语句并没有执行，因此，如果该数据操作符合完整性约束，则在触发器中需要重复该操作
```



