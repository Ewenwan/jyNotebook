1. Vue.js使用了基于HTML的模板语法，运行开发者声明式地将DOM绑定至底层Vue实例的数据
2. Vue.js的核心是一个运行采用简洁的模板语法来声明式的将数据渲染进DOM的系统

结合响应系统，在应用状态改变时，Vue能够智能地计算出重新渲染组件的最小代价并应用到DOM操作上

---

### 插值

##### 文本

数据绑定最常见的形式就是使用`{{....}}(双大括号)`的文本插值

```
<div id="test3">
  <p>{{message}}</p>
</div>
```

##### Html

使用v-html指令用于输出html代码

###### v-html

```
        <div id="test3">
            <p>{{message}}</p>
        </div>
        <script type="text/javascript">
            var v = new Vue({
                el:"#test3",
                data:{
                    message:"Hello Vue.js"
                }
            })
        </script>
```

##### 实例1

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test3</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test3">
            <p>{{message}}</p>
        </div>
        <script type="text/javascript">
            var v = new Vue({
                el:"#test3",
                data:{
                    message:"Hello Vue.js"
                }
            })
        </script>
    </body>
</html>
```

##### 属性

HTML属性中的值应使用v-bind指令

以下实例判断class1的值，如果为true使用class1类的样式，否则不使用该类

###### v-bind指令

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test4</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <style>
        .class1{
            background:#444;
            color:#eee;
        }
    </style>
    <body>
        <div id="test4">
            <label for="r1">修改颜色</label>
            <input type="checkbox" v-model="class1" id="r1" />
            <br /><br />
            <div v-bind:class="{'class1':class1}">
                v-bind:class 指令
            </div>
        </div>

        <script>
            new Vue({
                el:"#test4",
                data:{
                    class1:false
                }
            });
        </script>
    </body>
</html>
```

##### 表达式

Vue.js都提供了完全的JavaScript表达式支持

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test5</title>
        <script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
    </head>
    <body>
    <div id="test5">
        {{5+5}}<br>
        {{ ok ? 'YES' : 'NO' }}<br>
        {{ message.split('').reverse().join('') }}
        <div v-bind:id="'list-' + id">angle</div>
    </div>
        <script type="text/javascript">
            new Vue({
                el:"#test5",
                data:{
                    ok:true,
                    message:"Angle",
                    id: 1,
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.4-3.png)

##### 指令

指令是带有v-前缀的特殊属性

指令用于在表达式的值改变时，将某些行为应用到DOM上，实例

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test6">
            <p v-if="seen">看得到吗</p>
            <template v-if="ok">
                <h1>A</h1>
                <h2>B</h2>
                <h3>C</h3>
            </template>
        </div>
        <script>
            new Vue({
                el:"#test6",
                data:{
                    seen:false,
                    ok:true,
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.4-4.png)

这里，v-if指令将根据表达式seen的值\(true或false\)来决定是否插入p元素或者template元素

##### 参数

参数在指令后以冒号指明，例如，v-bind指令被用来响应地更新HTML属性

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test7</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test7">
            <pre><a v-bind:href="url">angle</a></pre>
        </div>

        <script>
            new Vue({
                el:"#test7",
                data:{
                    url:"http://www.python.org"
                }
            })
        </script>
    </body>
</html>
```

在这里href是参数，v-bind指令该元素的href属性与表达式url的值绑定

另一个例子是v-on指令，用于监听DOM事件

```
<a v-on:click="doSomething">
```

##### 修饰符

修饰符是以半角句号`.`指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent`修饰符告诉`v-on`指令对于触发的事件调用`event-preventDefault():`

```
<form v-on:submit.prevent="onSubmit"></form>
```

##### 用户输入

在input输入框中我们可以使用v-model指令来实现双向数据绑定

###### 双向数据绑定

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test8</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test8">
            <p> {{message}} </p>
            <input v-model="message">
        </div>

        <script>
            new Vue({
                el:"#test8",
                data:{
                    message:"angle"
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.4-5.png)

`v-model`指令用来在input、select、text、checkbox、radio等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

按钮的事件可以使用v-on监听事件，并对用户的输入进行响应

实例:在用户点击按钮后对字符串进行反转操作

###### 字符串反转

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test8</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test9">
            <p> {{message}} </p>
            <button v-on:click="reverseMessage">反转字符串</button>
        </div>

        <script>
            new Vue({
                el:"#test9",
                data:{
                    message:"angle",
                },
                methods:{
                    reverseMessage:function(){
                        this.message = this.message.split('').reverse().join('')
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果

![](/assets/1.13.4.4-6.png)

##### 过滤器

Vue.js运行自定义过滤器，被用作一些常见的文本格式化。由管道符指示，格式如下

```
<!-- 在两个大括号中 -->
{{ message|capitalize }}

<!-- 在v-bind指令中 -->
<div v-bind:id="rawId | formatId"></div>
```

过滤器函数接受表达式的值作为第一个参数

以下实例对输入的字符串第一个字符串转为大写

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test10</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test10">
            {{message|capitalize}}
        </div>

        <script>
            new Vue({
                el:"#test10",
                data:{
                    message:"angle"
                },
                filters:{
                    capitalize:function(value){
                        if(!value) return ''
                        value = value.toString()
                        return value.charAt(0).toUpperCase() + value.slice(1)
                    }
                }
            })
        </script>
    </body>
</html>
```

过滤器可以串联

```
{{message|filterA|filterB}}
```

过滤器是JavaScript函数，因此可以接受参数

```
{{message | filterA('arg1',arg2)}}
```

这里，message是第一个参数，字符串'arg1'将传给过滤器作为第二个参数，arg2表达式的值将被求值然后给过滤器作为第三个参数。

---

### 缩写

##### v-bind缩写

Vue.js为两个最为常用的指令提供了特别的缩写

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

##### v-on缩写

```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```



