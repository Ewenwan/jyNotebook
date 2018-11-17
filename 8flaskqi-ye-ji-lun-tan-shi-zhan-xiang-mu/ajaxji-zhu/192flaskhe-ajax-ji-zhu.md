```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- 原生JavaScript，使用XMLHttpRequest -->
    <!-- 使用jq:https://www.bootcdn.cn/jquery/ -->
    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
    <script>
        $(function () {
            $('#submit-btn').click(function (event) {
                event.preventDefault();

                {#$.ajax()#}
                {#$.get();#}
                {#$.post();#}
                var username = $('input[name="username"]').val();
                var password = $('input[name="password"]').val();
                $.post({
                    'url':'/login/',
                    'data':{
                        'username':username,
                        'password':password,
                    },
                    'success':function (data) {
                        if(data["code"] == 200){
                            window.location = '/';
                        }else{
                            {#window.alert(data["message"]);#}
                            var message = data["message"];
                            $("#message-p").html(message);
                            $("#message-p").show();
                        }
                    },
                    'fail':function (error) {
                        console.log(error);
                    }
                });
            });
        });
    </script>
</head>
<body>
<form action="" method="post">
    <table>
        <tr>
            <td>用户名:</td>
            <td><input type="text" name="username"></td>
        </tr>
        <tr>
            <td>密码:</td>
            <td><input type="password" name="password"></td>
        </tr>
        <tr>
            <td></td>
            <td>
                <button id="submit-btn">立即登陆</button>
            </td>
        </tr>
    </table>
    <p style="display: none;color: red;" id="message-p"></p>
</form>
</body>
</html>
```



```
from flask import Flask,render_template,request,url_for,redirect,jsonify

app = Flask(__name__)

# Ajax（ajax）
# Async JavaScript And XML
# Async（异步），网络请求是异步的
# JavaScript:JavaScriptt语言
# And:并且
# XML -> Json

@app.route('/')
def index():
    return 'Hello World!'

# 传统表单
@app.route('/login/',methods=["POST","GET"])
def login():
    if request.method == "GET":
        return render_template('login.html')
    else:
        # 和前端约定好，发送网络请求，不管是否验证成功
        # 都返回同样格式的json对象
        # {"code":code,"message":message}
        username = request.form.get("username")
        password = request.form.get("password")
        # return "username:{},password:{}".format(username,password)
        if username == "angle" and password == "123456":
            return jsonify({"code":200,"message":""})
        else:
            return jsonify({"code":401,"message":"用户名或密码错误"})
if __name__ == '__main__':
    app.run(debug=True)

```



