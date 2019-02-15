### 主流浏览器

* 浏览器:由shell和内核构成

  * IE:trident

  * Firefox:Gecko

  * Google Chrome:Webkit/blink
  * Safari:Webkit
  * Opera:presto

* 原因

  * 在市场上占有一定的份额
  * 拥有独立的内核

---

### 注释

* 由`<!-- -->构成，中间包括注释的内容`

* 功能
  * 备注,说明

### 引入css

* 行间样式

```
<div style="
			width: 100px;
			height: 100px;
			background: red;
			">
			
		</div>
```

* 页面级css

```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<title></title>
		
		<style type="text/css">
			
			*{
				margin: 0;
				padding: 0;
			}
			
			div{
				width: 100px;
				height: 100px;
				background: red;
			}
			
		</style>
		
	</head>
	<body>
		<div></div>
	</body>
</html>

```

* 外部css文件
  * 新建一个index.css，将css样式写入其中

```
div {
	width: 100px;
	height: 100px;
	background: red;
}
```

* 在index.html的head标签中使用link标签引入index.css文件

```
<head>
    <link href="index.css" rel="stylesheet" />
</head>
```



