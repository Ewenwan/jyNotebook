### 权重\(256进制\)

* !important:Infinity
* 行间样式:1000
* id:100
* class\|属性\|伪类:10
* 标签\|伪元素:1
* 通配符:0

### 选择器

* 父子选择器/派生选择器

```
<!DOCTYPE html>
<html lang="en">

	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			div strong em{
				background: red;
			}
		</style>
	</head>

	<body>
		<div><strong><em>angle</em></strong></div>
	</body>

</html>
```

![](/assets/14.2.10.2-01.png)

* 直接子元素选择器

```
section>(div>(p>a>span)+ul>(li>(a>span>em)+p)+li)+a>(p>em)+div
```

```
<!DOCTYPE html>
<html lang="en">

	<head>
		<meta charset="utf-8" />
		<title></title>
		<style type="text/css">
			section div ul li a em{
				background-color: red;
			}
		</style>
	</head>

	<body>
		<section>
			<div>
				<p><a href=""><span></span></a></p>
				<ul>
					<li>
						<a href=""><span><em>1</em></span></a>
						<p></p>
					</li>
					<li></li>
				</ul>
			</div>
			<a href="">
				<p><em>2</em></p>
				<div></div></a>
		</section>
	</body>

</html>
```



