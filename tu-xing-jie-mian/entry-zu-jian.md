* Entry组件:输入框

### 添加和删除文本

```
from tkinter import *

root = Tk()
e = Entry(root)
e.pack(padx=20,pady=20)
e.delete(0,END)
e.insert(0,"MIKU")
e.delete(0,END)

mainloop()
```

* Entry\(root\):创建一个输入框
* e.delete\(0,END\):0~END之间的数据
* e.insert\(0,text\):在0开始处插入一个文本值

### 获取输入框中的文本值

```
# from tkinter import *
#
# root = Tk()
# e = Entry(root)
# e.pack(padx=20,pady=20)
# e.delete(0,END)
# e.insert(0,"MIKU")
# e.delete(0,END)
#
# mainloop()


from tkinter import *

root = Tk()
# grid()方法允许用表格的形式来管理组件的位置
# row选项代表行，column选项代表列
Label(root,text="作品:").grid(row=0)
Label(root,text="作者:").grid(row=1)
v1 = StringVar()
e1 = Entry(root,textvariable=v1,show="*")
e2 = Entry(root)
e1.grid(row=0,column=1,padx=10,pady=5)
e2.grid(row=1,column=1,padx=10,pady=5)

def show():
    print("{}:{}".format(v1.get(),e2.get()))
    e1.delete(0,END)
    e2.delete(0,END)

# 如果表格大于组件，可以使用sticky选项来设置组件的位置
Button(root,text="获取",command=show,width=10).grid(row=3,column=0,sticky=W,padx=10,pady=5)
Button(root,text="退出",command=root.quit,width=10).grid(row=3,column=1,sticky=E,padx=10,pady=5)


mainloop()
```

* Entry组件的get\(\)方法能够获取输入框中文本值,即e2.get\(\)
* Entry\(root,textvariable=v1,show="\*"\)
  * show参数，可以隐藏原文本内容，实现其他指定字符
* grid\(row,column\):表格形式的布局

### 验证输入内容是否合法

Entry组件支持验证输入内容的合法性，实现验证合法性功能，需要通过设置validate,validatecommand和invalidcommand三个选项

```
from tkinter import *

root = Tk()

def test():
    if e1.get() == '1':
        print("正确")
        return True
    else:
        print("错误")
        return False

def test2():
    print("返回")
    return True

v = StringVar()
e1 = Entry(root,textvariable=v,validate="focusout",validatecommand=test,invalidcommand=test2)
# e2 = Entry(root)
e1.pack(padx=10,pady=10)
# e2.pack(padx=10,pady=10)

mainloop()
```

* validate选项

| 值 | 含义 |
| :--- | :--- |
| focus | 当Entry组件获得或失去焦点的时候验证 |
| focusin | 当Entry组件获得焦点的时候验证 |
| focusout | 当Entry组件失去焦点的时候验证 |
| key | 当出现上面任何一种情况的时候验证 |
| all | 当出现上面任何一种情况的时候验证 |
| none | 关闭验证功能，默认设置该选项\(即不启用验证\)。注意，是字符串的'none',而非None |

* validatecommand选项:指定一个验证函数，该函数只能返回True或者False表示验证的结果
* invalidcommand选项:该选项只有在validatecommand的返回值为False的时候才会被调用
* 额外选项

| 选项 | 含义 |
| :--- | :--- |
| %d | 操作代码:0表示删除操作，1表示插入操作，2表示获取、失去焦点或textvariable变量的值被修改 |
| %i | 当用户尝试插入或删除操作的时候，该选项表示插入或删除的位置\(索引号\)如果是由于获得、失去焦点或textvariable变量的值被修改而调用验证函数，那么该值是-1 |
| %P | 当输入框的值允许改变的时候，该值有效，该值为输入框的最新文本内容 |
| %s | 该值为调用验证函数前输入框的文本内容 |
| %S | 当插入或删除操作触发验证函数的时候，该值有效；该选项表示文本被插入和删除的内容 |
| %v | 该组件当前的validate选项的值 |
| %V | 调用验证函数的原因，该值是focusin,focusout,key或者forced\(textvariable选项指定的变量值被修改\)中的一个 |
| %W | 该组件的名字 |

```
from tkinter import *

root = Tk()

def test(content):
    if content == '1':
        print("正确")
        return True
    else:
        print("错误")
        return False

def test2():
    print("返回")
    return True

v = StringVar()
# 注意需要调用register()方法将验证函数包装起来
testCMD = root.register(test)
e1 = Entry(root,textvariable=v,validate="focusout",validatecommand=(testCMD,'%P'),invalidcommand=test2)
e2 = Entry(root)
e1.pack(padx=10,pady=10)
e2.pack(padx=10,pady=10)

mainloop()
```



