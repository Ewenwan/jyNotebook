* 组件（Component）是 Vue.js 最强大的功能之一
* 组件可以扩展 HTML 元素，封装可重用的代码

注册一个全局组件语法格式:

```
Vue.component(tagName,options)
```

tagName为组件名，options为配置选项。注册后，可以使用以下方式调用组件

```
<tagName></tagName>
```

### 全局组件

所有实例都能用全局组件

* 实例:注册一个简单的全局组件angle,并使用

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test44</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test44">
            <angle></angle>
        </div>

        <script type="text/javascript">
            Vue.component('angle',{
                template:"<p>自定义</p>"
            })

            new Vue({
                el:"#test44"
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.12-1.png)

### 局部组件

* 实例:注册一个简单的局部组件angle，并使用

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test45</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test45">
            <angle></angle>
        </div>

        <script type="text/javascript">
            var Child = {
                template:"<p>自定义</p>"
            }
            new Vue({
                el:"#test45",
                components:{
//                    'angle':Child
                    'angle': {
                            template:"<p>自定义</p>"
                        }
                }
            })
        </script>
    </body>
</html>
```

### Prop

prop是父组件用来传递数据的一个自定义属性

父组件的数据需要通过props把数据传给子组件，子组件需要显示的用props选项声明"prop"

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test46</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test46">
            <child message="hello!"></child>
        </div>

        <script>
            Vue.component('child',{
                props:["message"],
                template:"<span>{{message}}</span>"
            })

            new Vue({
                el:"#test46"
            })
        </script>
    </body>
</html>
```

#### 动态Prop

类似于用v-bind绑定HTML特性到一个表达式，也可以用v-bind动态绑定props的值父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test47</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test47">
            <div>
                <input v-model="parentMsg"/>
                <br />
                <child v-bind:message="parentMsg"></child>
            </div>
        </div>

        <script type="text/javascript">
            Vue.component('child',{
                props:["message"],
                template:"<span>{{message}}</span>"
            })

            new Vue({
                el:"#test47",
                data:{
                    parentMsg:"父组件内容"
                }
            })
        </script>
    </body>
</html>
```

* 将 v-bind 指令将 todo 传到每一个重复的组件中

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test49</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test49">
            <ol>
                <todo-item v-for="item in items" v-bind:todo="item"></todo-item>
            </ol>
        </div>

        <script type="text/javascript">
            Vue.component('todo-item',{
                props:["todo"],
                template:"<li>{{todo.text}}</li>"
            })

            new Vue({
                el:"#test49",
                data:{
                    items:[
                        {text:"angle"},
                        {text:"miku"},
                    ]
                }
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.12-5.png)

> 注意: prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来

### Prop验证

组件可以为props指定验证要求

prop是一个对象而不是字符串数组时，包含验证要求

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>test50</title>
            <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        </head>
        <body>
            <div id="test50">
                <my-child 
                    :num="100"
                    :msg="'angle'"
                    :object="{a:'a'}"
                    :cust="100"
                    >
                </my-child>
            </div>

                        <script type="text/javascript">
                    Vue.component('my-child',{
                        props:{
                            // 基础类型检测 (`null` 意思是任何类型都可以)
                            num:Number,
                            //多种类型
    //                        propB:[String,Number],
                            //必传且是字符串
                            msg:{
                                type:String,
                                required:true,
                            },
                            //数字，有默认值
                            num1:{
                                type:Number,
                                default:1000,
                            },
                            //数组/对象的默认值应当由一个工厂函数返回
                            object:{
                                type:Object,
                                default:function(){
                                    return {
                                        message:'hello'
                                        }
                                }
                            },
                            //自定义验证函数
                            cust:{
                                validator:function(value){
                                    return value > 10
                                }
                            }

                        },
                        template:"<div><p>{{num}}</p><p>{{msg}}</p><p>{{num1}}</p><p>{{object}}</p><p>{{cust}}</p></div>"
                    })
                    new Vue({
                        el:"#test50"
                    })
                </script>
        </body>
    </html>

type 可以是下面原生构造器：

* String
* Number
* Boolean
* Function
* Object
* Array
* type 也可以是一个自定义构造器，使用 instanceof 检测

### 自定义事件

父组件是使用props传递数据给子组件，但如果子组件要把数据传递回去，就需要使用自定义事件

可以使用v-on绑定自定义事件，每个Vue实例都实现了事件接口，即

* 使用$on\(eventName\)监听事件
* 使用$emit\(eventName\)触发事件

父组件可以在使用子组件的地方直接用v-on来监听子组件触发的事件

实例:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test51</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test51">
            <div id="counter-event-example">
                <p>{{ total }}</p>
                <button-counter v-on:increment="incrementTotal"></button-counter>
                <button-counter v-on:increment="incrementTotal"></button-counter>
            </div>
        </div>

        <script type="text/javascript">

            Vue.component('button-counter',{
                template:'<button v-on:click="incrementHandler">{{ counter }}</button>',
                data:function(){
                    return {
                        counter:0
                    }
                },
                methods:{
                    incrementHandler:function(){
                        this.counter += 1
                        this.$emit('increment')
                    }
                },
            })

            new Vue({
                el:"#test51",
                data:{
                    total:0
                },
                methods:{
                    incrementTotal:function(){
                        this.total += 1
                    }
                }
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.12-6.png)

如果你想在某个组件的根元素上监听一个原生事件。可以使用 .native 修饰 v-on 。例如：

```
<my-component v-on:click.native="doTheThing"></my-component>
```



