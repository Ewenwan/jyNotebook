### 1.相关链接

UEditor:[http://ueditor.baidu.com/website/](http://ueditor.baidu.com/website/)

下载地址:[http://ueditor.baidu.com/website/download.html\#ueditor](http://ueditor.baidu.com/website/download.html#ueditor)

文档:[http://fex.baidu.com/ueditor/](http://fex.baidu.com/ueditor/)

### 2.ueditor

文件下载

链接：[https://pan.baidu.com/s/1xUXaS24TIF3\_Z0plmyCx8A](https://pan.baidu.com/s/1xUXaS24TIF3_Z0plmyCx8A) 密码：lsxe

### 3.配置

```
import os

UEDITOR_UPLOAD_PATH = os.path.join(os.path.dirname(__file__),'images')
UEDITOR_UPLOAD_TO_QINIU = True
UEDITOR_QINIU_ACCESS_KEY = "xxxx-xxxx"
UEDITOR_QINIU_SECRET_KEY = "xxxxx"
UEDITOR_QINIU_BUCKET_NAME = "xxxx"
UEDITOR_QINIU_DOMAIN = 'http://pdhjzz2pa.bkt.clouddn.com/'
```

#### 4.首页

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="{{ url_for('static',filename='ueditor/ueditor.config.js') }}"></script>
    <script src="{{ url_for('static',filename='ueditor/ueditor.all.min.js') }}"></script>
    <title>Title</title>
</head>
<body>
    <script id="editor" type="text/plain"></script>
    <script>
        var ue = UE.getEditor("editor",{
            'serverUrl':'/ueditor/upload/',
        });
    </script>
</body>
</html>
```

### 5.后台

```
from flask import Flask,render_template
import qiniu,config
from ueditor import bp

app = Flask(__name__)
app.register_blueprint(bp)
app.config.from_object(config)

@app.route('/')
def hello_world():
    return render_template("index.html")


if __name__ == '__main__':
    app.run(debug=True)

```



