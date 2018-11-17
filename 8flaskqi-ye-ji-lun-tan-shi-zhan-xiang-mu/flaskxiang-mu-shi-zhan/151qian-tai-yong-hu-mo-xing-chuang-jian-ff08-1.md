```
用户模块:登录、注册...
```

为了隐藏用户的数量的显示，不要使用自动增长，应该使用随机字符串,而使用uuid的话，字符串过于太长，不便于查询等操作，而在保证同样的效果时，就使用shortuuid

### 安装

```
pip install shortuuid
```

### 定义模型

```
from exts import db
import shortuuid
from werkzeug.security import  generate_password_hash,check_password_hash
import enum
from datetime import datetime

class GenderEnum(enum.Enum):
    MALE = 1
    FEMALE = 2
    SECRET = 3
    UNKNOW = 4

# 为了隐藏用户的数量的显示，不要使用自动增长，应该使用随机字符串
# unique:保持唯一
class FrontUser(db.Model):
    __tablename__ = 'front_user'
    id = db.Column(db.String(100),primary_key=True,default=shortuuid.uuid)
    telephone = db.Column(db.String(11),nullable=False,unique=True)
    username = db.Column(db.String(50),nullable=False)
    _password = db.Column(db.String(100), nullable=False)
    email = db.Column(db.String(50),unique=True)
    realname = db.Column(db.String(50))
    avatar = db.Column(db.String(100))
    signature = db.Column(db.String(100))
    gender = db.Column(db.Enum(GenderEnum),default=GenderEnum.UNKNOW)
    join_time = db.Column(db.DateTime,default=datetime.now)

    def __init__(self,*args,**kwargs):
        if "password" in kwargs:
            self.password = kwargs.get('password')
            kwargs.pop("password")
        super(FrontUser,self).__init__(*args,**kwargs)

    # 将password函数定义为属性
    @property
    def password(self):
        return self._password

    # 通过werkzeug的内置has函数进行加密和解密，判断
    @password.setter
    def password(self,newpwd):
        self._password = generate_password_hash(newpwd)

    def check_password(self,rawpwd):
        return check_password_hash(self._password,rawpwd)
```



