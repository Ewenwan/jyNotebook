* ListBox组件:以列表形式显示，并支持滚动条操作

### 删除列表数据

```
from tkinter import *

root = Tk()
theLB = Listbox(root,setgrid=True)
theLB.pack()
# 向列表中添加数据
for i in range(100):
    theLB.insert(END,str(i))

# ACTIVE:是一个特殊的索引号，表示当前被选中的项目
theButton = Button(root,text="删除",command=lambda x=theLB:x.delete(ACTIVE))
theButton.pack()

mainloop()
```

* listbox.delete\(0,END\)

* listbox组件提供了四种选择模式:SINGLE\(单选\)、BROWSE\(单选、但拖动鼠标或通过方向键可以直接改变选项\)、MULTIPLE\(多选\)和EXTENDED\(多选，但需要同时按住Shift键或Ctrl键或拖动光标实现\)。默认的选择模式是BROWSE

* listbox\(root,height\)

  * height:设置列表的高度



