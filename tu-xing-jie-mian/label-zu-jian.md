* Label组件用于在界面上输出描述的标签

```
from tkinter import *

root = Tk()

# 创建一个文本对象
textLabel = Label(root,text="MIKU")
textLabel.pack(side=LEFT)

# 创建一个图像Label对象
# 用PhotoImage实例化一个图片对象(支持gif格式的图片)
photo = PhotoImage(file="1.gif")
imgLabel = Label(root,image=photo)
imgLabel.pack(side=RIGHT)


mainloop()
```

运行结果:

![](/assets/tk-6.1.1.2-1.png)

* Label\(root,text,justify,padx,image,compund,font=\(字体,字号\),fg\)
  * root:Tk\(\)实例化对象
  * text:文本内容
  * justify:设置水平对齐方式
  * padx:设置间隔距离
  * image:设置背景图片
  * compund:设置模式\(CENTER即设置文本和图像的混合模式\)
  * font:设置字体和字号
  * fg:设置文本颜色
* Label.pack\(side,padx,pady\):能够通过pack\(\)方法修改方位
  * side:设置水平位置\(LEFT,RIGHT,TOP,BOTTOM\)
  * padx:水平偏移
  * pady:垂直偏移

* mainloop\(\):进入主事件循环



