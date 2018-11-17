# 105 Flask-Restful参数验证

Flask-Restful插件提供了类似wtForms来验证提交的数据是否合法的包，叫做reqparse。

基本用法:

```text
parser = reqparse.RequestParser()
parser.add_argument('username',type=str,help='请输入用户名',required=True)
args = parser.parse_args()
```

add\_argument可以指定这个字段的名字，这个字段的数据类型等。

参数详细讲解:

1. default:默认值，如果这个参数没有值，那么将使用这个参数指定的值
2. required:是否必须，如果这个参数没有值，那么将使用这个参数指定的值
3. type:这个参数的数据类型，如果指定，那么将使用指定的数据类型来强制转换提交上来
4. choices:选项。提交上来的值只有满足这个选项中的值才符合验证通过，否则验证不通过
5. help:错误信息。如果验证失败后，将会使用这个参数指定的值作为错误信息
6. trim:是否要取出前后的空格

其中的type，可以使用python自带的一些数据类型，也可以使用flask\_restful.inputs下的一些特定的数据累心来强制转换。

常用的:

1. url:会判断这个参数的值是否是一个url，如果不是，就会抛出异常
2. regex:正则表达式
3. date:将这个字符串转换为datetime.date。如果转换不成功，则会抛出一个异常

```text
from flask import Flask,render_template,url_for
from flask_restful import Api,Resource,reqparse,inputs

app = Flask(__name__)
# 用Api来绑定app
api = Api(app)

# Json数据
class LoginView(Resource):
    def post(self):
        # username
        # password
        parser = reqparse.RequestParser()
        parser.add_argument('birthday', type=inputs, help='生日字段验证')
        # # 验证日期
        # parser.add_argument('birthday',type=inputs.date,help='生日字段验证')
        # # 利用正则表达式验证手机号码
        # parser.add_argument('telphone',type=inputs.regex(r'1[3578]\d{9}'))
        # # 验证输入的url地址
        # parser.add_argument('home_page',type=inputs.url,help='个人中心链接验证错误')
        # parser.add_argument('username',type=str,help='用户名验证错误',default="angle")
        # parser.add_argument('password',type=str,help=u'密码验证错误',required=True,trim=True)
        # parser.add_argument('password',type=int,help=u'年龄验证错误')
        # parser.add_argument('gender',type=str,choices=['male','female','secret'],help="性别验证错误")
        args = parser.parse_args()
        print(args)
        return {"username":'angle'}
api.add_resource(LoginView,'/login/')

# with app.test_request_context():
#     print(url_for('index',username='angle'))

if __name__ == '__main__':
    app.run(debug=True)
```

