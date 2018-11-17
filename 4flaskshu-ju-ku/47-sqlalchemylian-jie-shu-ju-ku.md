# 47 SQLAlchemy连接数据库

## SQLAlchemy介绍和使用

数据库是一个网站的基础，在Flask中可以自由的使用MySQL、PostgreSQL、SQLite、Redis、MongoDB来写原生的语句实现功能，也可以使用更高级别的数据库抽象方式，如SQLAlchemy或MongoEngine这样的OR\(D\)M。本教程以MySQL+SQLAchemy的组合来进行讲解

在讲解Flask中的数据库操作之前，先确保已经安装了以下软件:

* msyql:如果是在windows上，到官网下载。如果是Ubuntu，通过命令下载 sudo apt-get install mysql-server libmysqlclient-dev -yq进行下载安装。
* MySQLdb:MySQLdb是用python来操作mysql的包，因此通过pip来安装，命令如下:pip install mysql-python。python3上使用pip install pymysql代替
* SQLAlchemy:SQLAlchemy是一个数据库的ORM框架，安装命令:pip install SQLAlchemy

## 通过SQLAlchemy连接数据库

代码示例:

```text
from sqlalchemy import create_engine

# 数据库配置变量
HOSTNAME = "127.0.0.1"
POST = "3306"
DATABASE = "xt_flask"
USERNAME = "root"
PASSWORD = "123456"
# 地址
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}".format(USERNAME,PASSWORD,HOSTNAME,POST,DATABASE)

# 创建数据库引擎
engine = create_engine(DB_URI)

# 创建连接
with engine.connect() as conn:
    rs = conn.execute("select 1")
    print(rs.fetchone()[0])
```

首先从sqlalchemy中导入create\_engine,用这个函数来创建引擎，然后用engine.coonect\(\)来连接数据库。其中一个比较重要的一点是，通过create\_engine函数的时候，需要传递一个满足某种格式的字符串，对这个字符串的格式来进行解释：

```text
 dialect+driver://user:password@host:port/database
```

dialect是数据库的实现，比如MySQL、postgresql，sqlite，并且转换成小写，driver是python对应的驱动，如果不指定，会选择默认的驱动，比如mysql的默认驱动是MySQLdb。username是连接数据库的用户名，password是连接数据库的密码，host是连接数据库的域名，post是数据库监听的端口号，database是连接哪个数据库的名字

上例例子输出1，就说明连接成功

