# 71 Flask-SQLAlchemy下alembic的配置

## myapp.py

```text
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
import config

app = Flask(__name__)
app.config.from_object(config)
db = SQLAlchemy(app)

# alembic revision --autogenerate -m "第一次提交"
# alembic upgrade head

# alembic revision --autogenerate -m "add age column"
# alembic upgrade head
class User(db.Model):
    __tablename__ = "user"
    id = db.Column(db.Integer,primary_key=True,autoincrement=True)
    username = db.Column(db.String(50),nullable=False)
    age = db.Column(db.Integer)

@app.route('/')
def hello_world():
    return 'Hello World!'


if __name__ == '__main__':
    app.run(debug=True)
```

## config.py

```text
HOSTNAME = "127.0.0.1"
PORT = "3306"
DATABASE = "alembic_demo"
USERNAME = "root"
PASSWORD = "123456"
# dialect+dricer://username:password@host:port/database
DB_URI = "mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8".format(USERNAME,PASSWORD,HOSTNAME,PORT,DATABASE)

SQLALCHEMY_DATABASE_URI = DB_URI
```

## env.py

```text
....
import sys,os
sys.path.append(os.path.dirname(os.path.dirname(__file__)))
import myapp
....

target_metadata = myapp.db.Model.metadata
....
```

