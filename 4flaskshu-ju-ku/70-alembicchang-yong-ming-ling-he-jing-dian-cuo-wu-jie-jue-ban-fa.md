# 70 alembic常用命令和经典错误解决办法

续上...

7.命令和参数解释:

* init:创建一个alembic仓库
* revision:创建一个新的版本文件
* --autogenerate:自动将当前模型的修改，生成迁移脚本
* -m:本次迁移做了哪些修改，用户可以指定这个参数，方便回顾
* upgrade:将指定版本的迁移文档映射到数据库中，会执行版本文档中的upgrade函数
* head:代表当前的迁移脚本的版本号
* downgrade:会执行指定版本的迁移文档中的downgrade函数
* heads:展示当前可用的heads脚本文档
* history:列出所有的迁移版本及其信息
* current:展示当前数据库中的版本号

另外，在第一次执行的upgrade的时候，就会在数据库中创建一个alembic\_version表，这个表只会有一条数据，记录当前数据库映射的是哪个版本的迁移文件

## 经典错误:

| 错误描述 | 原因 | 解决办法 |
| :--- | :--- | :--- |
| FAILED:Target databases is not up to date | 主要是heads和current不相同。current落后于heads的版本 | 将current移动到head上。alembic upgrade head |
| FAILED:can't locate revision identified by 'xxxxx' | 数据库中存的版本号不在迁移脚本文档中 | 删除数据的alembic\_version表中的数据，重新执行alembic upgrade head |

```text
# head
代表最新版本的迁移脚本的版本号

alembic upgrade Revision ID

把数据映射到数据库中
alembic upgrade head

# 查看Revision ID
alembic heads

# 查看当前版本号
alembic current

# 更新字段/添加字段
alembic revision --autogenerate -m "add country column"
# 执行
alembic upgrade head

# 删除字段
alembic revision --autogenerate -m "delete contry column"
alembic upgrade head

# 查看所有历史消息
alembic history

# 降级
将数据库降级到最初版本
alembic downgrade base
将数据库降级到执行版本，使用alembic downgrade+版本号
alembic downgrade <version>
```



