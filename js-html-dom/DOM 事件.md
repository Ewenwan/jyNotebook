## 对事件做出反应

可以在事件发生时执行javascript，比如当用户在HTML元素上点击时

在用户点击某个元素时执行代码，向一个HTML事件属性添加javascript代码

```
onclick = Javascript
```

HTML事件例子:

* 当用户点击鼠标时
* 当网页已加载时
* 当图像已加载时
* 当鼠标移动到元素上时
* 当输入字段被改变时
* 当提交HTML表单时
* 当用户触发按键时

例子1:

当用户在&lt;h1&gt;元素上点击时，会改变其内容

```
<h1 onclick="this.innerHTML='谢谢!'">点击</h1>
```

例子2:

从事件处理器调用一个函数

```
<!DOCTYPE HTML>
<html>
    <head>
        <script>
            function changetext(id)
            {
                id.innerHTML = "谢谢"
            }
        </script>
    </head>
    <body>
        <h1 onclick="changtext(this)">点击</h1>
    </body>
</html>
```

---

## HTML 事件属性

向HTML元素分配事件，可以使用事件属性

实例:向button 元素分配onclick事件

```
<button onclick="displayDate()">点击</button>
```

---

## 使用HTML DOM来分配事件

HTML DOM允许通过使用javascript来向HTML元素分配事件

实例:向button元素分配onclick事件

```
<script>
    document.getElementById("myBtn").onclick = function(){dispalyDate()};
</script>
```

当按钮被点击时，会执行函数

---

## onload和onunload事件

onload和onunload事件会在用户进入或离开页面时被触发

onload事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本

onload和onunload事件可用于cookie

```
<!DOCTYPE HTML>
<html>
    <body onload="checkCookies()">
        <script>
            function checkCookies()
            {
                if(navigator.cookieEnabled == true)
                    alert("已启用cookie");
                else
                    alert("未启用cookie");

            }
        </script>
    </body>
</html>
```

---

## onchange事件

onchange事件长结合对输入字段的验证来使用

实例:当用户输入字段的内容时，会调用upperCase\(\)函数

```
<!DOCTYPE HTML>
<html>
    <head>
        <script>
        /*
            function myFunction()
            {
                var x = document.getElementById("fname");
                x.value = x.value.toUpperCase();
            }*/
            function myFunction()
            {
                id.value = id.value.toUpperCase();
            }
        </script>
    </head>
    <body>
        <!--<input type="text" id="fname" onchange="myFunction()" />-->
        <input type="text" onchange="myFunction(this)" />
    </body>
</html>
```

---

## onmouseover和onmouseout事件

onmouseover和onmouseout事件可用于在用户的鼠标移至HTML元素上方或移出元素时触发函数

实例:简单的onmouseover-onmouseout实例

```
<!DOCTYPE HTML>
<html>
    <body>
        <div style="background-color:green;width:120px;height:20px;padding:40px;color:white" onmouseout="mOut(this)" onmouseover="mOver(this)">
            把鼠标移到上面
        </div>

        <script>
            function mOver(obj)
            {    
                obj.innerHTML = "谢谢"
            }
            function mOut(obj)
            {
                obj.innerHTML = "把鼠标移到上面来"
            }
        </script>

    </body>
</html>
```

---

## onmousedown、onmouseup以及onclick事件

onmousedown、onmouseup以及onclick事件构成了鼠标点击事件的所有部分。当现实当点击鼠标按钮时，会触发onmousedown事件，当释放鼠标跑按钮时，会触发onmouseup事件，最后当完成鼠标点击时，会触发onclick事件

```
<html>
    <body>
        <div onmousedown="mDown(this)" onmouseup = "mUp(this)" style="background-color:green;color:white;width:90px;height:20px padding:40px;
        font-size:12px">点击</div>

        <script>
            function mDown(obj)
            {
                obj.style.backgroundColor="blue";
                obj.innerHTML = "清释放鼠标"
            }
            function mUp(obj)
            {
                obj.style.backgroundColor="green";
                obj.innerHTML = "请按下鼠标"
            }
        </script>
    </body>
</html>
```

---

## 事件句柄　\(Event Handlers\)

HTML 4.0 的新特性之一是能够使 HTML 事件触发浏览器中的行为，比如当用户点击某个 HTML 元素时启动一段 JavaScript。下面是一个属性列表，可将之插入 HTML 标签以定义事件的行为。

| 属性 | 此事件发生在何时... |
| :--- | :--- |
| [onabort](http://www.w3school.com.cn/jsref/event_onabort.asp) | 图像的加载被中断。 |
| [onblur](http://www.w3school.com.cn/jsref/event_onblur.asp) | 元素失去焦点。 |
| [onchange](http://www.w3school.com.cn/jsref/event_onchange.asp) | 改变&lt;select&gt;元素中的选项或其他表单失去焦点，并且在其获取焦点后内容发生过改变时触发 |
| [onclick](http://www.w3school.com.cn/jsref/event_onclick.asp) | 当用户点击某个对象时调用的事件句柄。 |
| [ondblclick](http://www.w3school.com.cn/jsref/event_ondblclick.asp) | 当用户双击某个对象时调用的事件句柄。 |
| [onerror](http://www.w3school.com.cn/jsref/event_onerror.asp) | 在加载文档或图像时发生错误。 |
| [onfocus](http://www.w3school.com.cn/jsref/event_onfocus.asp) | 元素获得焦点。 |
| [onkeydown](http://www.w3school.com.cn/jsref/event_onkeydown.asp) | 某个键盘按键被按下。 |
| [onkeypress](http://www.w3school.com.cn/jsref/event_onkeypress.asp) | 某个键盘按键被按下并松开。 |
| [onkeyup](http://www.w3school.com.cn/jsref/event_onkeyup.asp) | 某个键盘按键被松开。 |
| [onload](http://www.w3school.com.cn/jsref/event_onload.asp) | 一张页面或一幅图像完成加载。 |
| [onmousedown](http://www.w3school.com.cn/jsref/event_onmousedown.asp) | 鼠标按钮被按下。 |
| [onmousemove](http://www.w3school.com.cn/jsref/event_onmousemove.asp) | 鼠标被移动。 |
| [onmouseout](http://www.w3school.com.cn/jsref/event_onmouseout.asp) | 鼠标从某元素移开。 |
| [onmouseover](http://www.w3school.com.cn/jsref/event_onmouseover.asp) | 鼠标移到某元素之上。 |
| [onmouseup](http://www.w3school.com.cn/jsref/event_onmouseup.asp) | 鼠标按键被松开。 |
| [onreset](http://www.w3school.com.cn/jsref/event_onreset.asp) | 重置按钮被点击。 |
| [onresize](http://www.w3school.com.cn/jsref/event_onresize.asp) | 窗口或框架被重新调整大小。 |
| [onselect](http://www.w3school.com.cn/jsref/event_onselect.asp) | 文本被选中。 |
| [onsubmit](http://www.w3school.com.cn/jsref/event_onsubmit.asp) | 确认按钮被点击。 |
| [onunload](http://www.w3school.com.cn/jsref/event_onunload.asp) | 用户退出页面。 |

## 鼠标 / 键盘属性

| 属性 | 描述 |
| :--- | :--- |
| [altKey](http://www.w3school.com.cn/jsref/event_altkey.asp) | 返回当事件被触发时，"ALT" 是否被按下。 |
| [button](http://www.w3school.com.cn/jsref/event_button.asp) | 返回当事件被触发时，哪个鼠标按钮被点击。 |
| [clientX](http://www.w3school.com.cn/jsref/event_clientx.asp) | 返回当事件被触发时，鼠标指针的水平坐标。 |
| [clientY](http://www.w3school.com.cn/jsref/event_clienty.asp) | 返回当事件被触发时，鼠标指针的垂直坐标。 |
| [ctrlKey](http://www.w3school.com.cn/jsref/event_ctrlkey.asp) | 返回当事件被触发时，"CTRL" 键是否被按下。 |
| [metaKey](http://www.w3school.com.cn/jsref/event_metakey.asp) | 返回当事件被触发时，"meta" 键是否被按下。 |
| [relatedTarget](http://www.w3school.com.cn/jsref/event_relatedtarget.asp) | 返回与事件的目标节点相关的节点。 |
| [screenX](http://www.w3school.com.cn/jsref/event_screenx.asp) | 返回当某个事件被触发时，鼠标指针的水平坐标。 |
| [screenY](http://www.w3school.com.cn/jsref/event_screeny.asp) | 返回当某个事件被触发时，鼠标指针的垂直坐标。 |
| [shiftKey](http://www.w3school.com.cn/jsref/event_shiftkey.asp) | 返回当事件被触发时，"SHIFT" 键是否被按下。 |

## IE 属性

除了上面的鼠标/事件属性，IE 浏览器还支持下面的属性：

| 属性 | 描述 |
| :--- | :--- |
| cancelBubble | 如果事件句柄想阻止事件传播到包容对象，必须把该属性设为 true。 |
| fromElement | 对于 mouseover 和 mouseout 事件，fromElement 引用移出鼠标的元素。 |
| keyCode | 对于 keypress 事件，该属性声明了被敲击的键生成的 Unicode 字符码。对于 keydown 和 keyup 事件，它指定了被敲击的键的虚拟键盘码。虚拟键盘码可能和使用的键盘的布局相关。 |
| offsetX,offsetY | 发生事件的地点在事件源元素的坐标系统中的 x 坐标和 y 坐标。 |
| returnValue | 如果设置了该属性，它的值比事件句柄的返回值优先级高。把这个属性设置为 fasle，可以取消发生事件的源元素的默认动作。 |
| srcElement | 对于生成事件的 Window 对象、Document 对象或 Element 对象的引用。 |
| toElement | 对于 mouseover 和 mouseout 事件，该属性引用移入鼠标的元素。 |
| x,y | 事件发生的位置的 x 坐标和 y 坐标，它们相对于用CSS动态定位的最内层包容元素。 |

## 标准 Event 属性

下面列出了 2 级 DOM 事件标准定义的属性。

| 属性 | 描述 |
| :--- | :--- |
| [bubbles](http://www.w3school.com.cn/jsref/event_bubbles.asp) | 返回布尔值，指示事件是否是起泡事件类型。 |
| [cancelable](http://www.w3school.com.cn/jsref/event_cancelable.asp) | 返回布尔值，指示事件是否可拥可取消的默认动作。 |
| [currentTarget](http://www.w3school.com.cn/jsref/event_currenttarget.asp) | 返回其事件监听器触发该事件的元素。 |
| [eventPhase](http://www.w3school.com.cn/jsref/event_eventphase.asp) | 返回事件传播的当前阶段。 |
| [target](http://www.w3school.com.cn/jsref/event_target.asp) | 返回触发此事件的元素（事件的目标节点）。 |
| [timeStamp](http://www.w3school.com.cn/jsref/event_timestamp.asp) | 返回事件生成的日期和时间。 |
| [type](http://www.w3school.com.cn/jsref/event_type.asp) | 返回当前 Event 对象表示的事件的名称。 |



