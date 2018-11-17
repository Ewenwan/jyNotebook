## 富文本编辑器

* 借助富文本编辑器，管理员能够编辑出来一个包含HTML的页面，从而页面的显示效果，可以由管理员定义，而不用完全依赖于前期开发人员
* 此处以tinymce为例，其他富文本编辑器的使用可以自行学习
* 使用编辑器的显示效果为:

![](/assets/富文本编辑器.png)

### 下载安装富文本编辑器

```
pip install django-tinymce
```

### 应用到项目中

* 在settings.py 中为INSTALLED\_APPS添加编辑器应用

```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
    'tinymce',
]
```

* 在settings.py中添加编辑配置项

```
# 富文本
TINYMCE_DEFAULT_CONFIG = {
    'theme':'advanced',
    'width':'600',
    'height':'400',
}
```

* 在主urls.py中配置

```
url(r'^tinymce/',include('tinymce.urls'))
```

* 在应用中定义模型的属性

```
from django.db import models
from tinymce.models import  HTMLField

class Text(models.Model):
    str = HTMLField()
```

* 在后台管理界面中，就会显示富文本编辑器，而不是多行文本框

---

### 自定义使用

* 定义视图edit，用于显示编辑器并完成提交

```
def edit(request):
    return render(request,'html/editpage.html')
```

* 配置url

```
urlpatterns = [
    url(r'^edit/$',views.edit,name="edit")
]
```

* 创建模板editpage.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="/static/tiny_mce/tiny_mce.js"></script>
    <script type="text/javascript">
        tinyMCE.init({
            'mode':'textarea',
            'theme':'advanced',
            'width':400,
            'height':100,
        })
    </script>
</head>
<body>
    <form method="post" action="/saveEdit/">
        <input name="name" type="text"/><br />
        <textarea name="text">angle</textarea>
        <input type="submit" value="submit"/>
    </form>
</body>
</html>
```

* 定义视图saveEdit，接收请求，并更新文本

```
def saveEdit(request):
    name = request.POST['name']
    text = request.POST['text']
    context = {'name':name,'text':text}
    return render(request,'html/saveEdit.html',context)
```

* 添加url项

```
url(r'^saveEdit/$',views.saveEdit,name="saveEdit"),
```

* 定义模板saveEdit.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>title:{{ name }}</h1>
    <div>
        内容:{{ text }}
    </div>
</body>
</html>
```

* 富文本模板

```
tinyMCE.init({
    // General options
    mode : "textareas",
    theme : "advanced",
    plugins : "pagebreak,style,layer,table,save,advhr,advimage,advlink,emotions,iespell,inlinepopups,insertdatetime,preview,media,searchreplace,print,contextmenu,paste,directionality,fullscreen,noneditable,visualchars,nonbreaking,xhtmlxtras,template,wordcount,advlist,autosave",

    // Theme options
    theme_advanced_buttons1 : "save,newdocument,|,bold,italic,underline,strikethrough,|,justifyleft,justifycenter,justifyright,justifyfull,styleselect,formatselect,fontselect,fontsizeselect,fullscreen,code",
    theme_advanced_buttons2 : "cut,copy,paste,pastetext,|,search,replace,|,bullist,numlist,|,outdent,indent,blockquote,|,undo,redo,|,link,unlink,anchor,image,cleanup,|,insertdate,inserttime,preview,|,forecolor,backcolor",
    theme_advanced_buttons3 : "tablecontrols,|,hr,removeformat,visualaid,|,sub,sup,|,charmap,emotions,iespell,media,advhr,|,print,|,ltr,rtl",

    theme_advanced_toolbar_location : "top",
    theme_advanced_toolbar_align : "left",
    theme_advanced_statusbar_location : "bottom",
    theme_advanced_resizing : true,

    // Example content CSS (should be your site CSS)
    //content_css : "/css/style.css",

    template_external_list_url : "lists/template_list.js",
    external_link_list_url : "lists/link_list.js",
    external_image_list_url : "lists/image_list.js",
    media_external_list_url : "lists/media_list.js",

    // Style formats
    style_formats : [
        {title : 'Bold text', inline : 'strong'},
        {title : 'Red text', inline : 'span', styles : {color : '#ff0000'}},
        {title : 'Help', inline : 'strong', classes : 'help'},
        {title : 'Table styles'},
        {title : 'Table row 1', selector : 'tr', classes : 'tablerow'}
    ],

    width: '700',
    height: '400'

});
```



