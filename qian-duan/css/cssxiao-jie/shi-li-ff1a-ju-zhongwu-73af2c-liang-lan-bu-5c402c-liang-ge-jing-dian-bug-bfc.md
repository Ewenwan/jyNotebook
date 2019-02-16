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

### 两栏布局

利用position进行绝对定位，然后使用margin-left让出被占的内容位置

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" type="text/css" href="index2.css"/>
    </head>
    <body>
        <div class="right"></div>
        <div class="left"></div>
    </body>
</html>
```

```
*{
    margin: 0;
    padding: 0;
}

.right{
    position: absolute;
    right: 0;
    width: 100px;
    height: 100px;
    background-color: blue;
}

.left{
    margin-right: 100px;
    height: 100px;
    background-color:burlywood ;
}
```

![](/assets/14.2.10-5ada5.png)

### 父子元素的垂直时margin的问题

垂直时，子元素的margin-top值大于父元素的margin-top值，父元素会跟随子元素走

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="index2.css"/>
	</head>
	<body>
		<div class="wrapper">
			<div class="content">
				
			</div>
		</div>
	</body>
</html>

```

```
*{
	margin: 0;
	padding: 0;
}

.wrapper{
	margin-left: 100px;
	margin-top: 100px;
	width: 100px;
	height: 100px;
	background-color: black;
}

.content{
	margin-left: 50px;
	margin-top: 100px;
	width:50px;
	height: 50px;
	background-color: purple;
}

```



