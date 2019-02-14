## 全局事件属性

HTML 4 增加了通过事件触发浏览器中行为的能力，比如当用户点击某个元素时启动一段 JavaScript。

如果需要学习更多有关使用这些事件进行编程的内容，请学习我们的[JavaScript 教程](http://www.w3school.com.cn/js/index.asp)和[DHTML 教程](http://www.w3school.com.cn/dhtml/index.asp)。

下面的表格列出了可插入 HTML 5 元素中以定义事件行为的标准事件属性。

* [Window 事件属性 - Window Event Attributes](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp#Window_Event_Attributes)
* [表单事件 - Form Events](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp#Form_Events)
* [键盘事件 - Keybord Events](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp#Keybord_Events)
* [鼠标事件 - Mouse Events](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp#Mouse_Events)
* [媒介事件 - Media Events](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp#Media_Events)

new：HTML 5 中的新的事件属性。

## Window 事件属性

window 对象触发的事件。

适用于 &lt;body&gt; 标签：

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| onafterprint | script | 在打印文档之后运行脚本 |
| onbeforeprint | script | 在文档打印之前运行脚本 |
| onbeforeonload | script | 在文档加载之前运行脚本 |
| onblur | script | 当窗口失去焦点时运行脚本 |
| onerror | script | 当错误发生时运行脚本 |
| onfocus | script | 当窗口获得焦点时运行脚本 |
| onhaschange | script | 当文档改变时运行脚本 |
| onload | script | 当文档加载时运行脚本 |
| onmessage | script | 当触发消息时运行脚本 |
| onoffline | script | 当文档离线时运行脚本 |
| ononline | script | 当文档上线时运行脚本 |
| onpagehide | script | 当窗口隐藏时运行脚本 |
| onpageshow | script | 当窗口可见时运行脚本 |
| onpopstate | script | 当窗口历史记录改变时运行脚本 |
| onredo | script | 当文档执行再执行操作（redo）时运行脚本 |
| onresize | script | 当调整窗口大小时运行脚本 |
| onstorage | script | 当文档加载加载时运行脚本 |
| onundo | script | 当 Web Storage 区域更新时（存储空间中的数据发生变化时） |
| onunload | script | 当用户离开文档时运行脚本 |

## 表单事件

由 HTML 表单内部的动作触发的事件。

适用于所有 HTML 5 元素，不过最常用于表单元素中：

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| onblur | script | 当元素失去焦点时运行脚本 |
| onchange | script | 当元素改变时运行脚本 |
| oncontextmenu | script | 当触发上下文菜单时运行脚本 |
| onfocus | script | 当元素获得焦点时运行脚本 |
| onformchange | script | 当表单改变时运行脚本 |
| onforminput | script | 当表单获得用户输入时运行脚本 |
| oninput | script | 当元素获得用户输入时运行脚本 |
| oninvalid | script | 当元素无效时运行脚本 |
| onreset | script | 当表单重置时运行脚本。HTML 5 不支持。 |
| onselect | script | 当选取元素时运行脚本 |
| onsubmit | script | 当提交表单时运行脚本 |

## 键盘事件

由键盘触发的事件。

适用于所有 HTML 5 元素：

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| onkeydown | script | 当按下按键时运行脚本 |
| onkeypress | script | 当按下并松开按键时运行脚本 |
| onkeyup | script | 当松开按键时运行脚本 |

## 鼠标事件

由鼠标或相似的用户动作触发的事件。

适用于所有 HTML 5 元素：

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| onclick | script | 当单击鼠标时运行脚本 |
| ondblclick | script | 当双击鼠标时运行脚本 |
| ondrag | script | 当拖动元素时运行脚本 |
| ondragend | script | 当拖动操作结束时运行脚本 |
| ondragenter | script | 当元素被拖动至有效的拖放目标时运行脚本 |
| ondragleave | script | 当元素离开有效拖放目标时运行脚本 |
| ondragover | script | 当元素被拖动至有效拖放目标上方时运行脚本 |
| ondragstart | script | 当拖动操作开始时运行脚本 |
| ondrop | script | 当被拖动元素正在被拖放时运行脚本 |
| onmousedown | script | 当按下鼠标按钮时运行脚本 |
| onmousemove | script | 当鼠标指针移动时运行脚本 |
| onmouseout | script | 当鼠标指针移出元素时运行脚本 |
| onmouseover | script | 当鼠标指针移至元素之上时运行脚本 |
| onmouseup | script | 当松开鼠标按钮时运行脚本 |
| onmousewheel | script | 当转动鼠标滚轮时运行脚本 |
| onscroll | script | 当滚动元素滚动元素的滚动条时运行脚本 |

## 媒介事件

由视频、图像以及音频等媒介触发的事件。

适用于所有 HTML 5 元素，不过在媒介元素（诸如 audio、embed、img、object 以及 video）中最常用：

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| onabort | script | 当发生中止事件时运行脚本 |
| oncanplay | script | 当媒介能够开始播放但可能因缓冲而需要停止时运行脚本 |
| oncanplaythrough | script | 当媒介能够无需因缓冲而停止即可播放至结尾时运行脚本 |
| ondurationchange | script | 当媒介长度改变时运行脚本 |
| onemptied | script | 当媒介资源元素突然为空时（网络错误、加载错误等）运行脚本 |
| onended | script | 当媒介已抵达结尾时运行脚本 |
| onerror | script | 当在元素加载期间发生错误时运行脚本 |
| onloadeddata | script | 当加载媒介数据时运行脚本 |
| onloadedmetadata | script | 当媒介元素的持续时间以及其他媒介数据已加载时运行脚本 |
| onloadstart | script | 当浏览器开始加载媒介数据时运行脚本 |
| onpause | script | 当媒介数据暂停时运行脚本 |
| onplay | script | 当媒介数据将要开始播放时运行脚本 |
| onplaying | script | 当媒介数据已开始播放时运行脚本 |
| onprogress | script | 当浏览器正在取媒介数据时运行脚本 |
| onratechange | script | 当媒介数据的播放速率改变时运行脚本 |
| onreadystatechange | script | 当就绪状态（ready-state）改变时运行脚本 |
| onseeked | script | 当媒介元素的定位属性 \[1\] 不再为真且定位已结束时运行脚本 |
| onseeking | script | 当媒介元素的定位属性为真且定位已开始时运行脚本 |
| onstalled | script | 当取回媒介数据过程中（延迟）存在错误时运行脚本 |
| onsuspend | script | 当浏览器已在取媒介数据但在取回整个媒介文件之前停止时运行脚本 |
| ontimeupdate | script | 当媒介改变其播放位置时运行脚本 |
| onvolumechange | script | 当媒介改变音量亦或当音量被设置为静音时运行脚本 |
| onwaiting | script | 当媒介已停止播放但打算继续播放时运行脚本 |

\[1\]：定位属性的英文译文是：seeking attribute。

