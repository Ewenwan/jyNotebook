

* Scale组件:与Scrollbar组件类似，但是使用范围不尽相同
  * Scale组件主要是通过滑块来表示某个范围内的一个数字。可以通过修改选项设置范围以及分辨率\(精度\)
  * 创建指定范围的Scale组件，只需指定组件的from和to两个选项即可

实例1:

```
from tkinter import *

root = Tk()
Scale(root,from_=0,to=42).pack()
Scale(root,from_=0,to=200,orient=HORIZONTAL).pack()

mainloop()
```

实例2:

```
from tkinter import *

root = Tk()
s1 = Scale(root,from_=0,to=42,tickinterval=5,length=200,resolution=5,orient=VERTICAL)
s1.pack()
s2 = Scale(root,from_=0,to=200,orient=HORIZONTAL)
s2.pack()

def show():
    print(s1.get(),s2.get())

Button(root,text="获取位置",command=show).pack()

mainloop()
```

* Scale\(root,from\_,to,tickinterval,length,resolution,orient\)
  * from\_:从什么位置开始
  * to:到什么位置结束
  * tickinterval:设置刻度
  * length:长度
  * resolution:设置分辨率，即步长
  * orient:VERTICAL:垂直位置摆放，HORIZONTAL:水平位置摆放



