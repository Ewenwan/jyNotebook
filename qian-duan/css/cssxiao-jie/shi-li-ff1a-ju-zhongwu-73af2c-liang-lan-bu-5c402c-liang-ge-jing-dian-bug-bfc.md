### 居中五环

* circle.html

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="circle.css" />
	</head>
	<body>
		<div class="plat">
			<div class="circle1"></div>
			<div class="circle2"></div>
			<div class="circle3"></div>
			<div class="circle4"></div>
			<div class="circle5"></div>
		</div>
	</body>
</html>

```

* circle.css

```
*{
	margin: 0;
	padding: 0;
}

.plat{
	position: fixed;
	left: 30%;
	top: 50%;
	height: 185px;
	width: 380px;
}

.circle1,
.circle2,
.circle3,
.circle4,
.circle5{
	position: absolute;
	width: 100px;
	height: 100px;
	border: 10px solid black;
	border-radius: 50%;
}

.circle1{
	border-color: red;
	left: 0;
	top: 0;
}

.circle2{
	border-color: green;
	left:130px;
	top: 0px;
}

.circle3{
	border-color: yellow;
	left:260px;
	top: 0px;
}

.circle4{
	border-color: blue;
	left:65px;
	top: 65px;
}


.circle5{
	border-color: purple;
	left:195px;
	top: 65px;
}

```

![](/assets/14.2.10.4-01.png)

