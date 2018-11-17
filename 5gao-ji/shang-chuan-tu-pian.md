## 上传图片

* 当Django在处理文件上传的时候，文件数据被保存在request.FILES
* FILES中的每个键为&lt;input type="file" name="" /&gt;中的name
* 注意:FILES只有在请求的方法为post且提交的&lt;form&gt;带有enctype="multipart/form-data"的情况下才会包含数据。否则，FILES将为一个空的类似于字典的对象
* 使用模型处理上传文件:将属性定义成models.ImageFiled累心

```
class UploadFile(models.Model):
    picture = models.ImageField(upload_to='upfile/')
```

* 注意:如果属性类型为ImageField需要安装包Pilow

```
pip insatll pillow
```

* 图片存储路径
  * 在static目录下创建upfile文件夹
  * 图片上传后，会保存到"/static/upfile"文件夹
  * 打开settings.py文件，增加media\_root项

```
# 上传文件目录
MDETA_ROOT = os.path.join(BASE_DIR,r'static/upfile')
```

* 使用django后台管理，遇到imageField类型的属性会出现一个file框，完成文件上传

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form method="post" action="{% url 'myapp:savefile' %}" enctype="multipart/form-data">
        {% csrf_token %}
        <input type="file" name="file"/><br />
        <input type="submit" value="submit"/>
    </form>
</body>
</html>
```

配置路由:

```
from django.conf.urls import url,include
from . import views

app_name = 'myapp'

urlpatterns = [
    url(r'^index/$',views.index),
    url(r'^upfile/$',views.upfile,name="upfile"),
    url(r'^savefile/$',views.savefile,name='savefile'),

]
```

配置视图

    from django.http import HttpResponse
    from django.shortcuts import render

    # Create your views here.

    def index(request):
        return render(request,'index.html')

    def upfile(request):
        return render(request,'upfile.html')

    import os
    from test4.settings import  *
    def savefile(request):
        if request.method == 'POST':
            f = request.FILES['file']
            # 合成文件在服务器端的路径

            # 1
            filePath = os.path.join(MDETA_ROOT,f.name)

            # 2
         `  # filePath = os.path.join(MDETA_ROOT+"/image",f.name)
            with open(filePath,'wb') as fp:
                for info in f.chunks():
                    fp.write(info)
        return HttpResponse("上传成功")



