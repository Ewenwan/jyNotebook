### 什么是vue.js?

Vue.js（读音 /vjuː/, 类似于 view） 是一套构建用户界面的渐进式框架。

### 目的

Vue 只关注视图层， 采用自底向上增量开发的设计。

Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。

### 第一个例子

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>测试实例</title>
		<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>

	</head>
	
	<body>
		<div id="test">
			<p>{{ name }}</p>
		</div>
		

		<script>
			new Vue({
			  el: '#test',
			  data: {
			   name: 'Hello Vue.js!'
			  }
			})
		</script>
	</body>
</html>

```

运行结果:

![](/assets/1.13.4-1.png)

