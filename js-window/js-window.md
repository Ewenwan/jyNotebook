## 浏览器对象模型\(BOM\)

## window对象

浏览器窗口

所有javascript全局对象、函数以及变量均自动成为window对象的成员

全局变量是window对象的属性

全局函数是window对象的方法

```
window.document.getElementById("header");

等价

document.getElementById("header");
```

---

## window 尺寸

有三种方法能够确定浏览器窗口的尺寸\(浏览器的视口、不包括工具栏和滚动条\)

对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：

* window.innerHeight - 浏览器窗口的内部高度
* window.innerWidth - 浏览器窗口的内部宽度

对于 Internet Explorer 8、7、6、5：

* document.documentElement.clientHeight
* document.documentElement.clientWidth

或者

* document.body.clientHeight
* document.body.clientWidth

实用的 JavaScript 方案（涵盖所有浏览器）：

```
var w = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth
var h = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight
```

显示浏览器窗口的高度和宽度:\(不包括工具栏和滚动条\)

---

其他Window方法

* window.open\(\) - 打开新窗口
* window.clos\(\) - 关闭当前窗口
* window.moveTo\(\) - 移动当前窗口
* window.resizeTo\(\) - 调整当前窗口的尺寸



