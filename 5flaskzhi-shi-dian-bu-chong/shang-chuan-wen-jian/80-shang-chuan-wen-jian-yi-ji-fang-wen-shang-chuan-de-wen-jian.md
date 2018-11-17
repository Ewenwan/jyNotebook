# 80 上传文件以及访问上传的文件

1.注意上传文件时，在form表单需要指定enctype="multipart/form-data"，不然上传文件不成功

```text
    <form action="" method="post" enctype="multipart/form-data">
        <table>
            <tbody>
                <tr>
                    <td>头像:</td>
                    <td><input type="file" name="avatar"/></td>
                </tr>
                <tr>
                    <td>描述信息:</td>
                    <td><textarea name="desc"></textarea></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" value="提交"/></td>
                </tr>
            </tbody>
        </table>
    </form>
```

2.在后台获取上传文件，应该使用"request.files.get\("文件字段名"\)"

```text
# 获取文件
avatar = request.files.get("avatar")
```

3.考虑安全性，在保存文件前，先使用"werkzeug.utils.secure\_filename"来对上传的文件名来进行过滤

```text
# 将文件名，包装一下，避免发生安全隐患
filename = secure_filename(avatar.filename)
```

4.获取到上传文件后，使用"avatar.save\(路径\)"来保存文件

```text
UPLOAD_PATH = os.path.join(os.path.dirname(__file__),"upload")

avatar.save(os.path.join(UPLOAD_PATH,filename))
```

5.如何从服务器上读取一个文件，应该定义一个url，来获取指定的文件，在这个视图函数中，使用"send\_from\_directory\(文件的目录,文件名\)"来获取

```text
@app.route("/images/<filename>/")
def get_images(filename):
    # send_from_directory(path,文件名)
    return send_from_directory(UPLOAD_PATH,filename)
```

