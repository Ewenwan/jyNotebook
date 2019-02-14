## 拖放\(drag和drop\)

---

实例:

```HTML
<html>
    <head>
        <style type="text/css">
            #div1{
                width:198px;
                height:66px;
                padding:10px;
                border:1px solid #aaaaaa;
            }
        </style>
        <script type="text/javascript">
            function allowDrop(ev)
            {
                ev.preventDefault();
            }
            function drag(ev)
            {
                ev.dataTransfer.setData("Text",ev.target.id);
            }
            function drop(ev)
            {
                ev.preventDefault();
                var data = ev.dataTransfer.getData("Text");
                ev.target.appendChild(document.getElementById(data));
            }
        </script>
    </head>
    <body>
        <div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
        <br />
        <img id="drag1" src="http://www.w3school.com.cn//i/eg_dragdrop_w3school.gif" draggable="true"
        ondragstart="drag(event)"></img>
    </body>
</html>
```

---

* ## 把元素设置为可拖放

把一个元素设置为可拖放，把raggable属性设置为true

```HTML
<img draggable="true">
```

* ## 拖放的内容 - ondragstart和setData\(\)

规定元素被拖动时发生的事情

在上述例子中,ondragstart属性调用了一个drag\(event\)函数,规定拖动什么数据

dataTransfer.setData\(\)方法设置被拖动数据的数据类型和值

```HTML
function drag(ev)
{
    ev.dataTransfer.setData("text",ev.target.id);
}

*** id="drag1" --- 可拖动元素
<img id="drag1" src="http://www.w3school.com.cn//i/eg_dragdrop_w3school.gif" draggable="true"
ondragstart="drag(event)"></img>
```

---

* ## 拖到什么地方 - ondragover

ondragover事件规定被拖动的数据能够放置到何处

默认地，数据/元素无法放置到其他元素中。为了实现拖放，必须阻止元素的这种默认的处理方式

所以有ondragover事件的event.preventDefault\(\)方法完成

```HTML
event.preventDefault()
```

---

* ## 进行放置 - ondrop

当放开被拖数据时，会发生drop事件

在本例子中，ondrop属性调用了一个函数,drop\(event\)

```HTML
function drop(ev)
{
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChiled(document.getElementById(data));
}
```

_说明:_

1. 调用preventDefault\(\)来阻止数据的浏览器默认处理方式\(drop事件的默认行为是以链接形式打开\)
2. 通过dataTransfer.getData\(\)方法获得被拖的数据。该方法将返回在setData\(\)方法中设置为相同类型的任何数据
3. 被拖数据时被拖元素的id\("drag1"\)
4. 把被拖元素追加到放置元素中

---

## 来回拖动图片

```HTML
<!DOCTYPE html>
<html>	
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			#div1,#div2
			{
				float:left;
				width:200px;
				height:100px;
				margin:10px;
				padding:10px;
				border:1px solid red;
			}
		</style>
		<script type="text/javascript">
			function allowDrop(ev)
			{
				ev.preventDefault();
			}
			function drag(ev)
			{
				ev.dataTransfer.setData("Text",ev.target.id);
			}
			function drop(ev)
			{
				ev.preventDefault();
				var data=ev.dataTransfer.getData("Text");
				ev.target.appendChild(document.getElementById(data));
			}
		</script>
	</head>
	<body>
		<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
			<img src="http://www.w3school.com.cn/i/eg_dragdrop_w3school.gif"
				draggable="true" ondragstart="drag(event)" id="drag1"/>
		</div>
		<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
	</body>
</html>

```



