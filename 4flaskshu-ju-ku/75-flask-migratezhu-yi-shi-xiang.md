# 75 Flask-Migrate注意事项

```text
#encoding: utf-8

from flask_script import Manager
from myapp import app
from exts import db
from flask_migrate import Migrate,MigrateCommand
# 需要把映射数据库中的模型导入到manage.py文件中
from models import User

# 需要把映射到数据库中的模型导入到manage.py文件中
from models import User

manager = Manager(app)

# 用来绑定app和db到flask_migrate的
Migrate(app,db)
# 添加Migrate的所有子命令到db下
manager.add_command("db",MigrateCommand)

def add_user():
    pass

if __name__ == '__main__':
    manager.run()
```

