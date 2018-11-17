Vue要实现异步加载需要使用到vue-resource库

```
<script src="https://cdn.bootcss.com/vue-resource/1.5.1/vue-resource.min.js"></script>
```

### Get请求

get请求简单实例

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>get请求</title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
<script src="https://cdn.staticfile.org/vue-resource/1.5.1/vue-resource.min.js"></script>
	</head>
	<body>
		<div id="ajax1">
			<input type="button" @click="get()" value="点击异步获取数据(GET)"/>
		</div>
		<script type="text/javascript">
			window.onload = function(){
				var v = new Vue({
					el:"#ajax1",
					data:{
						msg:"HelloWorld"
					},
					methods:{
						get:function(){
							//发送请求
							this.$http.get('1.txt').then(function(res){
								document.write(res.body)
							},function(){
								console.log("请求失败处理")
							})
						}
					}
				})
			}
		</script>
	</body>
</html>

```

结果:

```
HelloWorlddasdadas
```

如果需要传递数据，可以使用 this.$http.get\('get.php',jsonData\) 格式，第二个参数 jsonData 就是传到后端的数据

```

```



