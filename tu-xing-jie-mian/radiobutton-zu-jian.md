* Radiobutton组件:单选按钮，要实现单选效果，同一组内的所有Radiobutton只能共享一个variable选项，并且需要设置不同的value选项值

实例1:

```
from tkinter import *

root = Tk()
v = IntVar()
Radiobutton(root,text="1",variable=v,value=1).pack(anchor=W)
Radiobutton(root,text="2",variable=v,value=2).pack(anchor=W)
Radiobutton(root,text="3",variable=v,value=3).pack(anchor=W)

mainloop()
```

实例2:

```
from tkinter import *

root = Tk()
params = [
    ["Python",1],
    ["Java",2],
    ["C++/C",3],
    ["C#",4],
]
v = IntVar()
v.set(1)
for value,i in params:
    Radiobutton(root,text=value,variable=v,value=i).pack(anchor=W)

mainloop()
```

实例3:

将勾选方式换为按钮的形式并且将整行都进行填充

```
from tkinter import *

root = Tk()
params = [
    ["Python",1],
    ["Java",2],
    ["C++/C",3],
    ["C#",4],
]
v = IntVar()
v.set(1)
for value,i in params:
    Radiobutton(root,text=value,variable=v,value=i,indicatoron=False).pack(fill=X)

mainloop()
```

* Radiobutton\(indicatoron\)
  * indicatoron:设为False，则勾选方式换为按钮的形式
  * pack\(fiill=X\)
    * fiil:参数值设置X，表示将整行都填充



