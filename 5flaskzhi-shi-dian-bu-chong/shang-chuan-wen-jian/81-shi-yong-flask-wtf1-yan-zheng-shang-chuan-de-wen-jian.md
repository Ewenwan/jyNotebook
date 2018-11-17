# 81 使用flask\_wtf1验证上传的文件

1.定义表单的时候，对文件的字段，需要采用"FileField"这个类型

2.验证器应该从"flask\_wtf.file"中导入，使用“flask\_wtf.file.FileRequired”是用来验证文件上传是否为空，“flask\_wtf.file.FileAllowed”用来验证上传的文件的后缀名

3.在视图文件中，使用"from werkzeug.datastructures.CombinedMultiDict"，来把"request.form"与"request.files"来进行合并，再传给表单来做验证

```text
form = UploadFrom(CombinedMultiDict([request.form,request.files]))
```

```text
upload.py

@app.route("/upload/",methods=["GET","POST"])
def upload():
    if request.method == "GET":
        return render_template("upload.html")
    else:
        form = UploadFrom(CombinedMultiDict([request.form,request.files]))
        if form.validate():
        # 通过form.字段名.data来获取数据
            desc = form.desc.data
            avatar = form.avatar.data
            filename = secure_filename(avatar.filename)
            avatar.save(os.path.join(UPLOAD_PATH,filename))
            print(os.path.join("\\".join(UPLOAD_PATH.split('/')),filename))
            return "文件上传成功"
        else:
            print(form.errors)
            return "fail"
```

```text
forms.py

from wtforms import Form,FileField,StringField
from wtforms.validators import  InputRequired
# flask_wtf
from flask_wtf.file import FileAllowed,FileRequired

class UploadFrom(Form):
    # 使用Flask - WTF提供的FileRequired、FileAllowed验证函数
    avatar = FileField(validators=[FileRequired(),FileAllowed(['jpg','png','gif'])])
    desc = StringField(validators=[InputRequired()])
```

