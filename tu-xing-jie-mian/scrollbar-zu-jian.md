* Scrollbar组件:滚动条，一般与其他组件配合使用
  * 为了使用垂直滚动条，需要做一些处理
    * 设置该组件的yscrollbarcommand选项为Scrollbar组件的set\(\)方法
    * 设置Scrollbar组件的command选项为该组件的yview\(\)方法

实例:

```
from tkinter import *

root = Tk()
sl = Scrollbar(root)
sl.pack(side=RIGHT,fill=Y)
lb = Listbox(root,yscrollcommand = sl.set)
for i in range(1000):
    lb.insert(END,str(i))

lb.pack(side=LEFT,fill=BOTH)
sl.config(command=lb.yview)

mainloop()
```

运行结果:

![](/assets/tk-6.1.1.9-1.png)





