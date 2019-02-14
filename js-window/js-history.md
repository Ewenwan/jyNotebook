## windwos History

方法:

history.back\(\) - 与浏览器点击后退按钮相同

history.forward\(\) - 与浏览器中点击按钮向前相同

---

## window history back

history.back\(\) 方法加载历史列表中的前一个URL

实例:在页面上创建后退按钮

```
<!DOCTYPE html>
<html>
	<head>
		<script>
			function goBack()
			{
				window.history.back();
			}
		</script>
	</head>
	<body>
		<input type="button" value="Back" onclick="goBack()"/>
	</body>
</html>
```

---

## Window History Forward

history forward\(\)方法加载历史列表中的下一个url

```
<!DOCTYPE html>
<html>
	<head>
		<script>
			function goForward()
			{
				window.history.forward();
			}
		</script>
	</head>
	<body>
		<button value="forward" type="button" onclick="goForward()">forward</button>
	</body>
</html>
```



