Indexs（索引是用来指向 Text 组件中文本的位置，跟 Python 的序列索引一样，Text 组件索引也是对应实际字符之间的位置

Tkinter 提供一系列不同的索引类型：

* line.column:行/列
* line.end:某一行的末尾
* INSERT	 
* CURRENT	 
* END	 
* user-defined marks	 
* user-defined tags\("tag.first", "tag.last"\)	 
* selection\(SEL\_FIRST, SEL\_LAST\)	 
* window coordinate\("@x,y"\)	 
* embedded object name\(window, images\)	 
* expressions

#### line.column

由于 Text 支持多行文本，就是从一维空间变成了二维空间。因此可以用行和列定位一个位置。

那么，行列就是最基础的索引方式，他们将索引位置的行号和列号以字符串的形式表示出来（中间以"."分隔，例如"1.0"表示第一列第一行）。需要注意的是，行号以1开始，列号以0开始。你还可以使用以下语法构建索引：

```
"%d.%d" % (line, column)
```

指定超出现有文本的最后一行的行号，或超出一行中列数的列号都不会引发错误。对于这样的指定，Tkinter 解释为已有内容的末尾的下一个位置。

需要注意的是，使用行列的索引方式看起来像是浮点值。其实不只是像而已，你在需要指定索引的时候使用浮点值代替也是可以的：

```
text.insert(INSERT, 'I LOVE STUDY')
print(text.get('1.2', 1.6))  #1.2  1.6可以不加双引号
```

使用 index\(\) 方法可以将所有支持的“索引”格式（上面写的那一大堆，11 个）转化为“行/列”格式的索引号

#### line.end

行号加上字符串 ".end" 的格式表示为该行最后一个字符的位置

```
text.insert(INSERT, 'I LOVE STUDY')
print(text.get('1.2', '1.END'))
#从第一行第三列到第一行最后
```

#### INSERT

INSERT 和下面两个有点类似 C 的宏定义

INSERT \(或 "insert" \)

对应插入光标的位置

#### CURRENT

CURRENT \(或 "current" \)  --用的少

对应与鼠标坐标最接近的位置。不过，如果你紧按鼠标任何一个按钮，它会直到你松开它才响应（即你松开时的位置）

#### END\(或"end"\)

对应 Text 组件的文本缓冲区最后一个字符的下一个位置

#### user-defined marks

user-defined marks 是对 Text 组件中位置的命名。INSERT 和 CURRENT 是两个预先命名好的 marks，除此之外你可以自定义 marks

#### User-defined tags\("tag.first", "tag.last"\)

User-defined tags 代表可以分配给 Text 组件的特殊事件绑定和风格。

你可以使用 "tag.first"（使用 tag 的文本的第一个字符之前）和 "tag.last"（使用 tag 的文本的最后一个字符之后）语法表示标签的范围。

```
"%s.first" % tagname
"%s.last" % tagname
```

如果查无此 tag，那么 Tkinter 会抛出 TclError 异常

#### selection\(SEL\_FIRST, SEL\_LAST\)

selection 是一个名为 SEL（或 "sel" ）的特殊 tag，表示当前被选中的范围，你可以使用 SEL\_FIRST 到 SEL\_LAST 来表示这个范围，如果没有选中的内容，那么 Tkinter 会抛出 TclError 异常

#### window coordinate\("@x,y"\)

你还可以使用窗口坐标作为索引。例如在一个事件绑定中，你可以使用以下代码找到最接近鼠标位置的字符：

```
"@%d,%d" % (event.x, event.y)
```

#### embedded object name\(window, images\)

embedded object name 用于指向在 Text 组件中嵌入的 window 和 image 对象。要引用一个 window，只要简单的将一个 Tkinter 组件实例作为索引即可。引用一个嵌入的 image，只需使用相应的 PhotoImage 和 BitmapImage 对象

#### expressions

expressions 用于修改任何格式的索引，用字符号的形式实现修改索引的表达式。

具体表达式实现如下：

* + count chars	
  * ①将索引向前\(-&gt;\)移动count个字符
  * ②可以越过换行符，但不能超过END的位置
* - count chars	
  * ①将索引向后\(&lt;-\)移动count个字符
  * ②可以越过换行符，但不能超过"1.0"的位置
* + count lines	
  * ①将索引向前\(-&gt;\)移动count行
  * ②索引会尽量保持与移动前在同一列上，但如果移动后的那一行字符太少，将移动到该行的末尾
* - count lines	
  * ①将索引向后\(&lt;-\)移动count行
  * ②索引会尽量保持与移动前在同一列上，但如果移动后的那一行字符太少，将移动到该行的末尾
* linestart
  * ①将索引移动到当前索引所在行的起始位置
  * ②注意，使用该表达式前边必须有一个空格隔开
* lineend	
  * ①将索引移动到当前索引所在行的末尾
  * ②注意，使用该表达式前边必须有一个空格隔开
* wordstart	
  * ①将索引移动到当前索引指向的单词的开头
  * ②单词的定义是一系列字母、数字、下划线或任何非空白字符的组合
  * ③注意，使用该该表达式前边必须有一个空格隔开
* wordend	
  * ①将索引移动到当前索引指向的单词的末尾
  * ②单词的定义是一系列字母、数字、下划线或任何非空白字符的组合
  * ③注意，使用该该表达式前边必须有一个空格隔开

ps.只要结果不产生歧义，关键字可以被缩写，空格也可以省略。例如："+ 5 chars" 可以简写成 "+5c"

在实现中，为了确保表达式为普通字符串，你可以使用 str 或格式化操作来创建一个表达式字符串。下面例子演示了如何删除插入光标前边的一个字符：

