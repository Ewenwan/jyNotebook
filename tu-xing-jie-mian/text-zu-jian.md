* Text组件:用于显示和处理多行文本，常常被用于作为简单的文本编辑器和网页浏览器使用

实例1:

```
from tkinter import *

root = Tk()
text = Text(root,width=50,height=30)
text.pack()
# INSERT索引表示插入光标当前的位置
text.insert(INSERT,"angle")
text.insert(END," miku")

mainloop()
```

运行结果:

![](/assets/tk-6.1.1.11-1.png)

实例2:

```
from tkinter import *

root = Tk()
text = Text(root,width=50,height=30)
text.pack()
text.insert(INSERT,"Angle")

def show():
    print("miku")

b = Button(text,text="点击",command=show)
text.window_create(INSERT,window=b)

mainloop()
```



