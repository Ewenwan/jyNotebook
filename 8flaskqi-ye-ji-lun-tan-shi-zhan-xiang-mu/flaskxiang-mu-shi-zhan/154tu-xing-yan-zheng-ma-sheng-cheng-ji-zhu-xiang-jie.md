### 生成验证码

```
import random,string
# Image:画布
# ImageDraw:画笔
# ImageFont:画笔的字体
# 相关库安装
# pip install pillow

from PIL import Image,ImageDraw,ImageFont

# Captcha验证码
class Captcha(object):
    # 生成几位数的验证码
    number = 4
    # 验证码图片的宽度和高度
    size = (100,30)
    # 验证字体大小
    fontsize = 25
    # 加入干扰线的条数
    line_number = 2

    # 构建一个验证码源文本
    SOURCE = list(string.ascii_letters)
    for index in range(0,10):
        SOURCE.append(str(index))

    # 填充颜色为150~255，颜色偏亮
    # 填充颜色为0~100，颜色偏暗
    # 随机生成的颜色
    @classmethod
    def __gene_random_color(cls,start=0,end=255):
        random.seed()
        # 随机生成3个0~255的参数以元组的形式返回
        return (random.randint(start,end),random.randint(start,end),random.randint(start,end))

    # 随机选择一个字体
    @classmethod
    def __gene_random_font(cls):
        fonts = [
            'Courgette-Regular.ttf',
            'LHANDW.TTF',
            'Lobster-Regular.ttf',
            'verdana.ttf'
        ]
        # 随机选择一个字体
        font = random.choice(fonts)
        return r'utils/captcha/'+font

    # 用来随机生成一个字符串(包括英文和数字)
    @classmethod
    def gene_text(cls,number):
        # number是生成验证码的位数
        return ''.join(random.sample(cls.SOURCE,number))

    # 绘制干扰线
    @classmethod
    def __gene_line(cls,draw,width,height):
        begin = (random.randint(0,width),random.randint(0,height))
        end = (random.randint(0,width),random.randint(0,height))
        draw.line([begin,end],fill=cls.__gene_random_color(),width=2)

    # 绘制干扰点
    @classmethod
    def __gene_points(cls,draw,point_chance,width,height):
        # 大小限制在[0~100]
        chance = min(100,max(0,int(point_chance)))
        for w in range(width):
            for h in range(height):
                tmp = random.randint(0,100)
                if tmp > 100 - chance:
                    draw.point((w,h),fill=cls.__gene_random_color())

    # 生成验证码
    @classmethod
    def gene_graph_captcha(cls):
        try:
            # 验证码图片的宽和高
            width,height = cls.size
            # 创建图片
            # R:red 0-255
            # G:green 0-255
            # B:blue 0-255
            # A:Alpha 0-255
            image = Image.new('RGBA',(width,height),cls.__gene_random_color(0,100))
            # 验证码的字体
            font = ImageFont.truetype(cls.__gene_random_font(),cls.fontsize)
            # 创建画笔
            draw = ImageDraw.Draw(image)
            # 生成字符串
            text = cls.gene_text(cls.number)
            # 获取字体的尺寸
            font_width,font_height = font.getsize(text)
            # 填充字符串
            # draw.text(x,y,fill)
            draw.text(((width-font_width)/2,(height-font_height)/2),text,font=font,fill=cls.__gene_random_color(150,255))
            # 绘制干扰线
            for x in range(0,cls.line_number):
                cls.__gene_line(draw,width,height)
            # 绘制噪点
            cls.__gene_points(draw,10,width,height)
        except:
            Captcha.gene_graph_captcha()
        return (text,image)

```

### 在视图中生成验证码

```
@bp.route('/captcha/')
def graph_captcha():
    try:
        # 获取验证码
        text,image = Captcha.gene_graph_captcha()
        # BytesIO,字节流
        # 获取图像，需要存入二进制流中
        out = BytesIO()
        # 保存在流中，并指定格式为png
        image.save(out,'png')
        out.seek(0)
        # response对象
        resp = make_response(out.read())
        resp.content_type = 'image/png'
    except:
        return graph_captcha()
    return resp
```



