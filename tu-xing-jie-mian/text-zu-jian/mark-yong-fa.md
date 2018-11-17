Marks（标记）通常是嵌入到 Text 组件文本中的不可见对象。事实上 Marks 是指定字符串间的位置，并跟随相应的字符一起移动。Marks 有 INSERT，CURRENT 和 user-defined marks（用户自定义 Marks）。其中，INSERT 和 CURRENT 是 Tkinter 预定义的特殊 Marks，他们不能被删除。

INSERT\(或 "insert"\) 用于指定当前插入光标的位置，Tkinter 会在该位置绘制一个闪烁的光标（因此，并不是所有的 Marks 都不可见）

CURRENT\(或 "current"\)用于指定对应与鼠标坐标最接近的位置。不过，如果你紧按鼠标任何一个按钮，它会直到你松开它才响应（即你松开时的位置）

你还可以自定义任意数量的 Marks，Marks 的名字是由普通字符串组成，可以是除了空白字符外的任何字符（为了避免歧义，你应该起一个有意义的名字）。使用 mark\_set\(\) 方法创建和移动 Marks。

如果你在一个 Mark 标记的位置之前插入或删除文本，那么 Marks 会跟着一起移动。删除 Marks 你需要使用 mark.unset\(\) 方法，删除 Marks 周围的文本并不会删除 Marks 本身

例一，Marks 事实上就是索引，用于表示位置：

```
text.insert(INSERT, 'I love study')
text.mark_set('here', '1.2') #第一行第三列做一个标记
text.insert('here', '插') #利用标记插入字符串

#原来的字符串变成'I 插love study'
```

例二，如果 Marks 前边的内容发生变化，那么 Mark 的位置也会跟着移动:

```
text.insert(INSERT, 'I love study')
text.mark_set('here', '1.2')
text.insert('here', '插')
text.insert('here', '入')

#原来的字符串变成'I 插入love study'
```

例三，如果 Marks 周围的文本被删除了，Marks 仍然还在：

```
text.insert(INSERT, 'I love study')
text.mark_set('here', '1.2')
text.insert('here', '插')

test.delete('1.0', END)
text.insert('here', '入')

#原来的字符串变成'入'
```

例四，只有 mark\_unset\(\) 方法可以解除对 Marks 的封印：

```
text.insert(INSERT, 'I love study')
text.mark_set('here', '1.2')
text.insert('here', '插')

text.mark_unset('here')

test.delete('1.0', END)
text.insert('here', '入')

#会报TclError的错误
```

默认插入内容到 Marks，是插入到它的左边（就是说插入一个字符的话，Marks 向后移动了一个字符的位置）。

那能不能插入到 Marks 的右侧呢（即 Marks 的位置一直不变）？其实是可以的，通过 mark\_gravity\(\) 方法就可以实现：

```
text.insert(INSERT, 'I love study')

text.mark_set('here', '1.2')
text.mark_gravity('here', LEFT)  #默认是RIGHT，也就是说插入一个数据，Marks默认是在这个数据的右边，即可能会（插入数据在Marks的右边时）相对插入前Marks的位置移动了一个。

text.insert('here', '插')
text.insert('here', '入')

#结果是"I 入插love study"
```

运行结果:

```
#结果是"I 入插love study"
```

不难总结出，Index 索引和 Marks 标记都是主要用于定位。Marks 可以看做是特殊的 Index，是一个可以自定义名字的 Index。但是他们又不是完全相同的，比如说在默认的情况下，在 Marks 指定的位置中插入数据，Marks 的位置会自动发生改变。

