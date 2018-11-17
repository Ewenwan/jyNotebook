* LabelFrame组件:是Frame框架的进化版，并且使Checkbutton和RadioButton的组件分组变得更加简单了

实例1:

```
from tkinter import *

root = Tk()
group = LabelFrame(root,text="最好的编程语言是?",padx=5,pady=5)
group.pack(padx=10,pady=10)
params = [
    ["Python",1],
    ["Java",2],
    ["C++/C",3],
    ["C#",4],
]
v = IntVar()
v.set(1)
for value,i in params:
    # 将RadioButton组件放到group窗口中
    Radiobutton(group,text=value,variable=v,value=i).pack(anchor=W)

mainloop()
```



