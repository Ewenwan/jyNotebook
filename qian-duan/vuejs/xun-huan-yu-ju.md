循环使用v-for指令

v-for指令需要以site in sites 形式的特殊语法，sites是源数据数组并且site是数组元素迭代的别名

v-for可以绑定数据到数组来渲染一个列表

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test15</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test15">
            <ol>
                <li v-for="site in sites">
                    {{site.name}}
                </li>
            </ol>
        </div>
        <script>
            new Vue({
                el:"#test15",
                data:{
                    sites:[
                        {name:"angle"},
                        {name:"miku"},
                    ]
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.6-1.png)

### v-for 迭代对象

* v-for可以通过一个对象的属性来迭代数据

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test16</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test16">
            <ul>
                <li v-for="value in object">
                    {{value}}
                </li>
            </ul>
        </div>

        <script>
            new Vue({
                el:"#test16",
                data:{
                    object:{
                        name:'angle',
                        url:'www.python.org',
                        slogan:'天使'
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.6-2.png)

* 可以提供第二个的参数为键名

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test17</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test17">
            <li v-for="(value,key) in object">
                {{key}}:{{value}}
            </li>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test17",
                data:{
                    object:{
                        name:'angle'
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.6-3.png)

* 第三个参数为索引

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test18</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test18">
            <li v-for="(value,key,index) in object">
                {{index}}.{{key}}:{{value}}
            </li>
        </div>

        <script type="text/javascript">
            new Vue({
                el:'#test18',
                data:{
                    object:{
                        name:'angle',
                        age:18
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.6-4.png)

#### v-for迭代整数

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>test19</title>
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
	</head>
	<body>
		<div id="test19">
			<ul>
				<li v-for="n in 10">
					{{n}}
				</li>
			</ul>
		</div>
		<script>
			new Vue({
				el:"#test19",
			})
		</script>
	</body>
</html>

```

运行结果

![](/assets/1.13.4.6-5.png)

