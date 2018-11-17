* Button组件:用于实现一个按钮，大部分参数与Label组件一样，并且可以接收信息，Button组件有一个command选项，可以实现

实例:

当按钮被点击后，文本内容发送改变

```
from tkinter import *


def callback():
    var.set("内容发生改变了")

root = Tk()

frame1 = Frame(root)
frame2 = Frame(root)

# 创建一个文本对象
var = StringVar()
var.set("原内容")

textLabel = Label(frame1,textvariable=var,justify=LEFT)
textLabel.pack(side=LEFT)
# 创建一个图像对象
photo = PhotoImage(file="1.gif")
imgLabel = Label(frame1,image=photo)
imgLabel.pack(side=RIGHT)

# 添加一个按钮
theButton = Button(frame2,text="点击改变内容",command=callback)
theButton.pack()
frame1.pack(padx=0,pady=10)
frame2.pack(padx=10,pady=10)

mainloop()
```

运行结果:

![](/assets/tk-6.1.1.3-1.png)                       ![](/assets/tk-6.1.1.3-2.png)

* Button\(command=func\)
  * func:点击时触发事件调用的函数
* Frame\(root\):创建一个框架



