_tips:通过HTML DOM，可访问javascript HTML文档的所有元素_

## HTML dom\(文档对象模型\)

当王爷被加载时，浏览器会创建页面的文档队形模型\(Document Object Model\)

HTML DOM 模型被构造为对象的树

### HTML DOM 树

![](http://www.w3school.com.cn/i/ct_htmltree.gif "DOM HTML 树")

通过可编程的对象模型，javascript获得了足够的能力来创建动态的HTML

* javascript能够改变页面中的所有HTML元素
* javascript能够改变页面中的所有HTML属性
* javascript能够改变页面中的所有css样式
* javascript能够对页面中的所有事件做出反应

---

## 查找HTML元素

通常，通过javascript，需要操作HTML元素

为了做到这件事情，必须首先找到该元素。有三种方法来做这件事

* 通过id找到HTML元素
* 通过标签名找到HTML元素
* 通过类名找到HTML元素

---

## 通过id查找HTML元素

在dom中查找HTML元素的最简单的方法，是通过使用元素的id

实例:本例查找id="intro"元素

```
var x = document.getElementById("intro");
```

如果找到该元素，则该方法将以对象\(在x中\)的形式返回该元素

如果未找到该元素，则x将包含null

---

## 通过标签名查找HTML元素

实例:通过id="main"，然后查找"main"中的所有&lt;p&gt;元素

```
var x = document.getELementById("main");
var y = x.getElementsByTagName("p);
```



