Tags（标签）通常用于改变 Text 组件中内容的样式和功能。你可以修改文本的字体、尺寸和颜色。另外，Tags 还允许你将文本、嵌入的组件和图片与鼠标和键盘等事件相关联。除了 user-defined tags（用户自定义的 Tags），还有一个预定义的特殊Tags：SEL。

SEL （或 "sel"）用于表示对应的选中内容（如果有的话）。

可以自定义任意数量的 Tags，Tags 的名字是由普通字符串组成，可以是除了空白字符以外的任何字符。另外，任何文本内容都支持多个 Tags 描述，任何 Tag 也可以用于描述多个不同的文本内容。

为指定文本添加 Tags 可以使用 tag\_add\(\) 方法：

```
text.insert(INSERT, 'I love study very well')
text.tag_add('tag1', '1.7', '1.12', '1.14')  #第一个参数是tag的名字，之后的参数是范围。这些参数表示的范围是'1.7'到'1.12'和一个单独的'1.14'
#光是这样只是在指定位置标注了一个tag标签，还需要对这些标签进行设置
text.tag_config('tag1', background='yellow', foreground='red')  
 
#字符串'I love study very well'中'study'和'e'颜色改变
```

### 设置样式

如上，使用 tag\_config\(\) 方法可以设置 Tags 的样式。下面罗列了 tag\_config\(\) 方法可以使用的选项：

* background
  * ①指定该Tag所描述的内容的背景颜色
  * ②注意：bg并不是该选项的缩写，在这里bg被解释成bgstipple选项的缩写
* bgstipple
  * ①指定一个位图作为背景，并使用background选项指定的颜色填充
  * ②只有设定了background选项，该选项才会生效
  * ③默认的标准位图有：'error', 'gray75', 'gray50', 'gray25', 'gray12', 'hourglass', 'info', 'questhead', 'question'和'warning'
* borderwidth
  * ①指定文本框的宽度
  * ②默认值是0
  * ③只有设定了relief选项该选项才会生效
  * ④注意：该选项不能使用bd缩写
* fgstipple
  * ①指定一个位图作为前景色
  * ②默认的标准位图有：'error', 'gray75', 'gray50', 'gray25', 'gray12', 'hourglass', 'info', 'questhead', 'question'和'warning'
* font    
  * ①指定该Tag所描述的内容使用的字体
* foreground
  * ①指定该Tag所描述的内容使用的前景色
  * ②注意：fg并不是该选项的缩写，在这里fg被解释为fgstipple的缩写
* justify
  * ①控制文本的对齐方式
  * ②默认是LEFT（左对齐），还可以选择RIGHT（右对齐）和CENTER（居中）
  * ③注意：需要将Tag指向该行的第一个字符，该选项才能生效
* Imargin1
  * ①设置Tag指向的文本块第一行的缩进
  * ②默认值是0
  * ③注意：需要将Tag指向该行的第一个字符或整个文本块，该选项才能生效
* Imargin2
  * ①设置Tag指向的文本块除了第一行其他行的缩进
  * ②默认值是0
  * ③注意：需要将Tag指向整个文本块，该选项才能生效
* offset
  * ①设置Tag指向的文本相对于基线的偏移距离
  * ②可以控制文本相对于基线是升高（正数值）或者降低（负数值）
  * ③默认值是0
* overstrike
  * ①在Tag指定的文本范围画一条删除线
  * ②默认值是False
* relief
  * ①指定Tag对应范围的文本的边框样式
  * ②可以使用的值有：SUNKEN，RAISED，GROOVE，RIDGE或FLAT
  * ③默认值是FLAT（没有边框）
* margin
  * ①设置Tag指向的文本块右侧的缩进
  * ②默认值是0
* spacing1
  * ①设置Tag所描述的文本块中每一行与上方的文本间隔
  * ②注意：自动换行不算
  * ③默认值是0
* spacing2
  * ①设置Tag所描述的文本块中自动换行的各行间的空白间隔
  * ②注意：换行符（"\n"）不算
  * ③默认值是0
* spacing3
  * ①设置Tag所描述的文本块中每一行与下方的文本间隔
  * ②注意：自动换行不算
  * ③默认值是0
* tabs
  * ①定制Tag所描述的文本块中Tab按键的功能
  * ②默认Tab被定义为8个字符的宽度
  * ③你还可以定制多个制表位：tabs=\('3c', '5c', '12c'\)表示前三个Tab的宽度分别为3cm，5cm，12cm，接着的Tab按照最后两个的差值计算，即：19cm，26cm，33cm
  * ④你应该注意到，它上边'c'的含义是“厘米”而不是“字符”，还可以选择的单位有"i"\(英寸\)，"m"（毫米），"p"（DPI，大约是'1i'等于'72p'）
  * ⑤如果是一个整型值，则单位是像素
* underline
  * ①该选项设置为True的话，则Tag所描述的范围内的文本将被画上下划线
  * ②默认值是False
* wrap
  * ①设置当一行文本的长度超过width选项设置的宽度时，是否自动换行。
  * ②该选项的值可以是：NONE（不自动换行），CHAR（按字符自动换行）和WORD（按单词自动换行）

如果你对同一个范围内的文本加上多个 Tags（会形成一个栈的形式），并且设置相同的选项，那么新建的 Tag 样式会覆盖比较旧的 Tag：

```
from tkinter import *

root = Tk()

text = Text(root, width=30, height=5)
text.pack()

text.insert(INSERT, 'I love study very well')
text.tag_add('tag1', '1.7', '1.12', '1.14')
text.tag_add('tag2', '1.7', '1.12', '1.14')
#注意这里是创建的顺序起决定性的作用

text.tag_config('tag2', foreground='blue')
text.tag_config('tag1', background='yellow', foreground='red')
#最后的前景色是蓝色，背景色还是黄色

mainloop()
```

### 设置Tag优先级

你或许想控制 Tags 间的优先级，这可以实现么？

你可以使用 tag\_raised\(\) 和 tag\_lower\(\) 方法来提高和降低某个 Tag 的优先级。

```
from tkinter import *

root = Tk()

text = Text(root, width=30, height=5)
text.pack()

text.tag_config('tag2', foreground='blue')  #设置tag的选项时，如果没有该tag，则会新建一个
text.tag_config('tag1', background='yellow', foreground='red') #此时这个就是新建的Tag的顺序
#到这里是黄底红字的

text.tag_lower('tag1')
#到这里就成了黄底蓝字

text.insert(INSERT, 'I love study very well', ('tag2', 'tag1'))  #和这里的tag选项的顺序无关。这样Tag加入的是整个文本

mainloop()
```



