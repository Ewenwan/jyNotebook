* Checkbox组件:多选按钮

实例1:

```
from tkinter import *

root = Tk()

# 需要一个Tkinter变量，用于表示该按钮是否被选中
# 选中得到值为1，否则为0
v = IntVar()
c = Checkbutton(root,text="测试",variable=v)
c.pack()
# 如果选项被选中，那么变量v被赋值为1，否则为0
label = Label(root,textvariable=v)
label.pack()

mainloop()
```

实例2:

```
from tkinter import *

root = Tk()

nums = [i for i in range(10)]
v = []
for num in nums:
    v.append(IntVar())
    b = Checkbutton(root,text=num,variable=v[-1])
    b.pack(anchor=W)


mainloop()
```

* IntVar\(\):Tkinter变量，用于表示是否按钮被选中

* anchor:用于指定显示位置，可选参数\(,N,NE,E,SE,S,SW,W,NW,CENTER\)



