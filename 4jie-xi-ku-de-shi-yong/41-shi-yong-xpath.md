# 4.1 使用xpath

## 1.说明

XPath，全称 XML Path Language，即 XML 路径语言，它是一门在XML文档中查找信息的语言。XPath 最初设计是用来搜寻XML文档的，但是它同样适用于 HTML 文档的搜索

## 2.相关链接

官方文档:[https://www.w3.org/TR/xpath/](https://www.w3.org/TR/xpath/)

## 3.XPath常用规则 {#2-xpath常用规则}

| 表达式 | 描述 |
| :--- | :--- |
| nodename | 选取此节点的所有子节点 |
| / | 从当前节点选取直接子节点 |
| // | 从当前节点选取子孙节点 |
| . | 选取当前节点 |
| .. | 选取当前节点的父节点 |
| @ | 选取属性 |

## 4. 实例引入 {#4-实例引入}

```text
from lxml import etree

content = '''
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
'''
# 调用etree模块的HTML类构造一个XPath解析对象
html = etree.HTML(content)
result = etree.tostring(html)
print(result.decode('utf-8'))
```

HTML 文本中的最后一个 li 节点是没有闭合的，但是 etree 模块可以对 HTML 文本进行自动修正

运行结果:

```text
<html><body><div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </li></ul>
 </div>
</body></html>
```

可以直接读取文本进行解析

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = etree.tostring(html)
print(result.decode('utf-8'))
```

test.html内容

```text
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
```

解析后结果:

```text
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/REC-html40/loose.dtd">
<html><body><div>&#13;
    <ul>&#13;
         <li class="item-0"><a href="link1.html">first item</a></li>&#13;
         <li class="item-1"><a href="link2.html">second item</a></li>&#13;
         <li class="item-inactive"><a href="link3.html">third item</a></li>&#13;
         <li class="item-1"><a href="link4.html">fourth item</a></li>&#13;
         <li class="item-0"><a href="link5.html">fifth item</a>&#13;
     </li></ul>&#13;
 </div></body></html>
```

## 5.所有结点

利用//开头的xpath规则选取所有符合要求的节点

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//*')
print(result)
```

\*代表匹配所有的结点

运行结果:

```text
[<Element html at 0x185591fd548>, <Element body at 0x185591fd688>, <Element div at 0x185591fd6c8>, <Element ul at 0x185591fd708>, <Element li at 0x185591fd748>, <Element a at 0x185591fd7c8>, <Element li at 0x185591fd808>, <Element a at 0x185591fd848>, <Element li at 0x185591fdac8>, <Element a at 0x185591fd788>, <Element li at 0x185591fdb08>, <Element a at 0x185591fdb48>, <Element li at 0x185591fdb88>, <Element a at 0x185591fdbc8>]
```

只获取li节点

要选取所有 li 节点可以使用 //，然后直接加上节点的名称即可，调用时直接调用 xpath\(\) 方法即可提取

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li')
print(result)
```

## 6.子结点

通过/或者//查找子结点或子孙子结点

实例:查找li节点下的所有a子节点

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li/a')
print(result)
```

运行结果:

```text
[<Element a at 0x1dc63e8d708>, <Element a at 0x1dc63e8d748>, <Element a at 0x1dc63e8d788>, <Element a at 0x1dc63e8d7c8>, <Element a at 0x1dc63e8d808>]
```

实例:查找ul节点下的所有的子孙a节点

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li//a')
print(result)
```

运行结果与上个例子是相同的

一定要注意/和//的区别，/是获取直接子节点，//是获取子孙节点

## 7. 父节点 {#7-父节点}

可以通过..来获取父节点

实例:获取href 是 link4.html 的 a 节点的父节点的class属性

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/../@class')
print(result)
```

运行结果:

```text
['item-1']
```

也可以通过 parent:: 来获取父节点

实例:

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/parent::*/@class')
```

## 8. 属性匹配 {#8-属性匹配}

@符号可以进行匹配属性

实例:

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]')
print(result)
```

运行结果为:

```text
[<Element li at 0x1e85c0bd748>, <Element li at 0x1e85c0bd788>]
```

## 9. 文本获取 {#9-文本获取}

利用xpath中的text\(\)方法可以获取节点中的文本

实例:获取li节点下的文本

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]/text()')
print(result)
```

运行结果:

```text
['\r\n     ']
```

可是没有到获取想要文本，是因为文本内容时在a节点下的，不能直接获取

而想获取其中的内容有两种方式，一种是选取到a节点再获取文本，另一种就是使用//

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]/a/text()')
print(result)
```

运行结果:

```text
['first item', 'fifth item']
```

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]//text()')
print(result)
```

运行结果:

```text
['first item', 'fifth item', '\r\n     ']
```

* 如果要想获取子孙节点内部的所有文本，可以直接用 // 加 text\(\) 的方式获取，能保证获取到最全面的文本信息，但可能会夹杂一些换行符等特殊字符
* 想获取某些特定子孙节点下的所有文本，先选取到特定的子孙节点，然后再调用 text\(\) 方法获取其内部文本，这样可以保证获取的结果是整洁的

## 10. 属性获取 {#10-属性获取}

获取属性的内容

实例:获取li节点下所有a节点的href属性

```text
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li/a/@href')
print(result)
```

运行结果:

```text
['link1.html', 'link2.html', 'link3.html', 'link4.html', 'link5.html']
```

## 11. 属性多值匹配 {#11-属性多值匹配}

匹配有多个属性值的节点，需要用contains\(\)函数

语法:

```text
contains(@属性名称,属性值)
```

例子:

```text
from lxml import etree

text = '''
<li class="li li-first"><a href="link.html">first item</a></li>
'''
html = etree.HTML(text)
result = html.xpath('//li[contains(@class,"li")]/a/text()')
print(result)
```

运行结果:

```text
['first item']
```

## 12. 多属性匹配 {#12-多属性匹配}

根据多个属性才能确定一个节点，需要使用运算符and来连接

```text
from lxml import etree

text = '''
<li class="li li-first" name="item"><a href="link.html">first item</a></li>
'''
html = etree.HTML(text)
result = html.xpath('//li[contains(@class,"li") and @name="item"]/a/text()')
print(result)
```

运行结果:

```text
['first item']
```

XPath 中的运算符，另外还有很多运算符，如 or、mod 等等，在此总结如下：

| 运算符 | 描述 | 实例 | 返回值 |
| :--- | :--- | :--- | :--- |
| or | 或 | price=9.80 or price=9.70 | 如果 price 是 9.80，则返回 true。如果 price 是 9.50，则返回 false。 |
| and | 与 | price&gt;9.00 and price&lt;9.90 | 如果 price 是 9.80，则返回 true。如果 price 是 8.50，则返回 false。 |
| mod | 计算除法的余数 | 5 mod 2 | 1 |
| + | 加法 | 6 + 4 | 10 |
| - | 减法 | 6 - 4 | 2 |
| \* | 乘法 | 6 \* 4 | 24 |
| div | 除法 | 8 div 4 | 2 |
| = | 等于 | price=9.80 | 如果 price 是 9.80，则返回 true。如果 price 是 9.90，则返回 false。 |
| != | 不等于 | price!=9.80 | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| &lt; | 小于 | price&lt;9.80 | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| &lt;= | 小于或等于 | price&lt;=9.80 | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| &gt; | 大于 | price&gt;9.80 | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| &gt;= | 大于或等于 | price&gt;=9.80 | 如果 price 是 9.90，则返回 true。如果 price 是 9.70，则返回 false。 |

参考来源：[http://www.w3school.com.cn/xpath/xpath\_operators.asp](http://www.w3school.com.cn/xpath/xpath_operators.asp)

## 13. 按序选择 {#13-按序选择}

实例:

```text
from lxml import etree

text = '''
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
'''
html = etree.HTML(text)
result = html.xpath('//li[1]/a/text()')
print(result)
result = html.xpath('//li[last()]/a/text()')
print(result)
result = html.xpath('//li[position()<3]/a/text()')
print(result)
result = html.xpath('//li[last()-2]/a/text()')
print(result)
```

第一次选择,选取了第一个 li 节点，中括号中传入数字1即可，注意这里和代码中不同，序号是以 1 开头的，不是 0 开头的。

第二次选择,选取了最后一个 li 节点，中括号中传入 last\(\) 即可，返回的便是最后一个 li 节点。

第三次选择,选取了位置小于 3 的 li 节点，也就是位置序号为 1 和 2 的节点，得到的结果就是前 2 个 li 节点。

第四次选择,选取了倒数第三个 li 节点，中括号中传入 last\(\)-2即可，因为 last\(\) 是最后一个，所以 last\(\)-2 就是倒数第三个。

运行结果如下：

```text
['first item']
['fifth item']
['first item', 'second item']
['third item']
```

函数参考:[http://www.w3school.com.cn/xpath/xpath\_functions.asp](http://www.w3school.com.cn/xpath/xpath_functions.asp)

## 13. 节点轴选择 {#13-节点轴选择}

```text
from lxml import etree

text = '''
<div>
    <ul>
         <li class="item-0"><a href="link1.html"><span>first item</span></a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
'''
html = etree.HTML(text)
# 获取所有祖先节点
result = html.xpath('//li[1]/ancestor::*')
print(result)
# 获取div的祖先节点
result = html.xpath('//li[1]/ancestor::div')
print(result)
# 获取属性值
result = html.xpath('//li[1]/attribute::*')
print(result)
# 获取直接子节点
result = html.xpath('//li[1]/child::a[@href="link1.html"]')
print(result)
# 获取所有子孙节点
result = html.xpath('//li[1]/descendant::span')
print(result)
# 获取当前节点之后的所有节点
result = html.xpath('//li[1]/following::*[2]')
print(result)
# 获取当前节点之后的所有同级节点
result = html.xpath('//li[1]/following-sibling::*')
print(result)
```

轴的使用，用法参考：[http://www.w3school.com.cn/xpath/xpath\_axes.asp](http://www.w3school.com.cn/xpath/xpath_axes.asp)

