### 条件判断

#### v-if

条件判断使用v-if指令:

* 在元素和template中使用v-if指令

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test11</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test11">
            <p v-if="seen">看的到吗</p>
            <template v-if="ok">
                <h1>A</h1>
                <h2>B</h2>
                <h3>C</h3>
            </template>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test11",
                data:{
                    seen:true,
                    ok:false,
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.5-1.png)

这里，v-if指令将根据表达式seen的值\(true或false\)来决定是否插入p元素

在字符串模板中，如

```
<!-- Handlebars模板 -->
{{#if ok}}
    <h1>Yes</h1>
{{/if}}
```

#### v-else

可以用v-else指令给v-if添加一个'else'块

实例:随机生成一个数字，判断是否大于0.5，然后输出对应信息

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test12</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test12">
            <div v-if="Math.random() > 0.5">
                Sorry
            </div>
            <div v-else>
                Not Sorry
            </div>
        </div>

        <script>
            new Vue({
                el:"#test12"
            })
        </script>
    </body>
</html>
```

#### v-else-if

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test13</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test13">
            <div v-if="type === 'A'">
                A
            </div>
            <div v-else-if="type === 'B'">
                B
            </div>
            <div v-else-if="type === 'C'">
                C
            </div>
            <div v-else>
                NOT A/B/C
            </div>
        </div>

        <script>
            new Vue({
                el:"#test13",
                data:{
                    type:"D"
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.5-2.png)

#### v-show

使用v-show指令来根据条件展示元素

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>test14</title>
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
	</head>
	<body>
		<div id="test14">
			<h1 v-show="ok">Hello!</h1>
		</div>
		
		<script>
			new Vue({
				el:"#test14",
				data:{
					ok:true,
				}
			})
		</script>
	</body>
</html>

```



