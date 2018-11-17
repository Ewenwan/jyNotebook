# 79 使用WTForms渲染模版

form还可以渲染模板

## 创建一个SettingsForm类

```text
class SettingsForm(Form):
    username = StringField("用户名",validators=[InputRequired()])
    age = IntegerField("年龄",validators=[NumberRange(0,100)])
    remember = BooleanField("记住")
    tags = SelectField("标签",choices=[("1","python"),("2","java"),("3","c++")])
```

可以通过form对象调用一些方法，将表单写好

```text
myapp.py

form = SettingsForm()
return render_template("settings.html",form=form)


settings.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        .username-input{
            background-color: red;
        }
    </style>
</head>
<body>
    <form action="" method="post">
        <table>
            <tbody>
                <tr>
                    <td>{{ form.username.label }}</td>
{#                    <td><input type="text" name="username"/></td>#}
                    <td>{{ form.username(class="username-input") }}</td>
                </tr>
                <tr>
                    <td>{{ form.age.label }}</td>
                    <td>{{ form.age() }}</td>
                </tr>
                <tr>
                    <td>{{ form.remember.label }}</td>
                    <td>{{ form.remember() }}</td>
                </tr>
                <tr>
                    <td>{{ form.tags.label }}</td>
                    <td>{{ form.tags() }}</td>
                </tr>
                <tr>
                    <td></td>
                    <td><input type="submit" value="提交"/></td>
                </tr>
            </tbody>
        </table>
    </form>
</body>
</html>
```

