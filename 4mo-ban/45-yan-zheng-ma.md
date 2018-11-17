## 验证码

* 在用户注册、登录页面，为了防止暴力请求，可以加入验证码功能，如果验证码错误，则不需要继续处理，可以减轻一些服务器的压力
* 使用验证码也是一种有效的防止crsf的方法
* 验证码效果如下图:

![](/assets/1245.png)

---

### 验证码视图

* 定义vrrifycode函数视图
* 使用pillow，pip install pillow
* Image标识画布对象
* ImageDraw表示画笔对象
* ImageFont表示字体对象
* 代码如下:

```
from django.http import HttpResponse
def verifycode(request):
    #引入绘图模块
    from PIL import Image, ImageDraw, ImageFont
    #引入随机函数模块
    import random
    #定义变量，用于画面的背景色、宽、高
    bgcolor = (random.randrange(20, 100), random.randrange(
        20, 100), 255)
    width = 100
    height = 25
    #创建画面对象
    im = Image.new('RGB', (width, height), bgcolor)
    #创建画笔对象
    draw = ImageDraw.Draw(im)
    #调用画笔的point()函数绘制噪点
    for i in range(0, 100):
        xy = (random.randrange(0, width), random.randrange(0, height))
        fill = (random.randrange(0, 255), 255, random.randrange(0, 255))
        draw.point(xy, fill=fill)
    #定义验证码的备选值
    str1 = 'ABCD123EFGHIJK456LMNOPQRS789TUVWXYZ0'
    #随机选取4个值作为验证码
    rand_str = ''
    for i in range(0, 4):
        rand_str += str1[random.randrange(0, len(str1))]
    #构造字体对象
    font = ImageFont.truetype('arial.ttf', 36)
    #构造字体颜色
    fontcolor = (255, random.randrange(0, 255), random.randrange(0, 255))
    #绘制4个字
    draw.text((5, 2), rand_str[0], font=font, fill=fontcolor)
    draw.text((25, 2), rand_str[1], font=font, fill=fontcolor)
    draw.text((50, 2), rand_str[2], font=font, fill=fontcolor)
    draw.text((75, 2), rand_str[3], font=font, fill=fontcolor)
    #释放画笔
    del draw
    #存入session，用于做进一步验证
    request.session['verifycode'] = rand_str
    #内存文件操作
    from io import BytesIO
    buf = BytesIO()
    #将图片保存在内存中，文件类型为png
    im.save(buf, 'png')
    #将内存中的图片数据返回给客户端，MIME类型为图片png
    return HttpResponse(buf.getvalue(), 'image/png')--
```

---

## 配置url

* 在urls.py中配置路由，请求验证码视图的url

```
from django.conf.urls import url,include
from . import views

app_name = 'myapp'

urlpatterns = [

    url('^image/$',views.verifycode),
]
```

---

## 显示验证码

* 在模板中使用img标签，src指向验证码视图

```
<img id='verifycode' src="/verifycode/" alt="CheckCode"/>
```

* 启动服务器，查看显示成功
* 扩展:点击"看不清，换一个"时，可以换一个新的验证码

```
<script type="text/javascript" src="/static/jquery-1.12.4.min.js"></script>
<script type="text/javascript">
    $(function(){
        $('#verifycodeChange').css('cursor','pointer').click(function() {
            $('#verifycode').attr('src',$('#verifycode').attr('src')+1)
        });
    });
</script>
<img id='verifycode' src="/verifycode/?1" alt="CheckCode"/>
<span id='verifycodeChange'>看不清，换一个</span>
```

* 为了能够实现提交功能，需要增加form和input标签

```
<form method='post' action='/verifycodeValid/'>
    <input type="text" name="vc">
    <img id='verifycode' src="/verifycode/?1" alt="CheckCode"/>
<span id='verifycodeChange'>看不清，换一个</span>
<br>
<input type="submit" value="提交">
</form>
```

---

## 验证

* 接收请求的信息，与session中的内容对比

```
def verifycodeValid(request):
    name = request.POST['name']
    if name.upper() == request.session['verifycode']:
        return HttpResponse('ok')
    else:
        return HttpResponse('no')
```

---

## 完整代码

login.html模板

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

    <form method="post" action="{% url 'myapp:verifycodeValid' %}">
        {% csrf_token %}
        <input type="text" name="name"><br />
        <img src="verifycode" srcset="{% url 'myapp:verifycode' %}?1" alt="CheckCode"/>
        <span id="verifycodeChange">看不清，换一个</span><br />
        <input type="submit" value="submit"/>
    </form>

    <script type="text/javascript">
        $(function () {
            $('#verifycodeChange').css('cursor','pointer').click(function () {
                $('#verifycode').attr('src',$('#verifycode').attr('src')+1)
            });
        });
    </script>
</body>
</html>
```

views.py视图

```
from django.http import HttpResponse
def verifycode(request):
    # 引入绘图模块
    from PIL import Image,ImageDraw,ImageFont
    # 引入随机函数模块
    import random
    # 定义变量，用于画面的背景色、宽、高
    # random.randrange(start,stop,step)，随机选取一个
    bgcolor = (random.randrange(20,100),random.randrange(20,100),255)
    width = 200
    height = 50
    # 创建画面对象
    im = Image.new('RGB',(width,height),bgcolor)
    # 创建画笔对象
    draw = ImageDraw.Draw(im)
    # 调用画笔的point()函数绘制噪点
    for i in range(0,100):
        xy = (random.randrange(0,width),random.randrange(0,height))
        fill = (random.randrange(0,255),255,random.randrange(0,255))
        draw.point(xy,fill=fill)
    # 定义验证码的备选值
    str1 = 'ABCD123EFGHIJK456LMNOPQRS789TUVWXYZ0'
    # 随机选取4个值作为验证码
    rand_str = ""
    for i in range(0,4):
        rand_str += str1[random.randrange(0, len(str1))]
    # 构造字体对象
    font = ImageFont.truetype('arial.ttf', 36)
    # 构造字体颜色
    fontcolor = (255,random.randrange(0,255),random.randrange(0,255))
    # 绘制4个字
    draw.text((5,2),rand_str[0],font=font,fill=fontcolor)
    draw.text((25, 2), rand_str[1], font=font, fill=fontcolor)
    draw.text((50, 2), rand_str[2], font=font, fill=fontcolor)
    draw.text((75, 2), rand_str[3], font=font, fill=fontcolor)
    #释放画笔
    del draw
    # 存入session，用于做进一步验证
    request.session['verifycode'] = rand_str
    # 内存文件操作
    from io import BytesIO
    buf = BytesIO()
    # 将图片保存在内存中，文件类型为png
    im.save(buf,'png')
    # 将内存中的图片数据返回给客户端，MIME类型为图片png
    return HttpResponse(buf.getvalue(),'image/png')


def verifycodeValid(request):
    name = request.POST['name']
    if name.upper() == request.session['verifycode']:
        return HttpResponse('ok')
    else:
        return HttpResponse('no')


def login(request):
    return render(request,'myapp/login.html')
```

urls.py配置路由

```
    url(r'^login/$',views.login,name="login"),

    url('^image/$',views.verifycode,name="verifycode"),
    url(r'^verifycodeValid/$',views.verifycodeValid,name="verifycodeValid"),
```



