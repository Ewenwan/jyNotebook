

### 溢出容器

* 单行文本:将多余文本以...形式显示

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="index2.css"/>
	</head>
	<body>
		<p>
			简介：毕生浮沉在相遇与离别的浪潮之间。但美中不足的，往往是该爱的时候太吝啬，该恨的时候又太留情。不管怎样，还望你和
 			我都能爱恨分明，别隐藏爱意，也别留下
		</p>
	</body>
</html>

```

```
*{
	margin: 0;
	padding: 0;
}

p{
	width: 300px;
	height: 80px;
	line-height: 20px;
	border: 1px solid black;
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}

```

* 多行文本



