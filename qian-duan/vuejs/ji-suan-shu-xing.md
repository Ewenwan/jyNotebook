* 计算属性关键词:computed
* 计算属性在处理一些复杂逻辑时是很有用的

实例1:反转字符串

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test20</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test20">
            {{message.split('').reverse().join('')}}
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test20",
                data:{
                    message:"angle",
                }
            })
        </script>
    </body>
</html>
```

运行结果:

```
elgna
```

实例2:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test21</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test21">
            <p>原始字符串:{{message}}</p>
            <p>计算机后反转字符串:{{reversedMessage}}</p>
        </div>

        <script type="text/javascript">
            var v = new Vue({
                el:"#test21",
                data:{
                    message:"Angle",
                },
                computed:{
                    //计算属性的getter
                    reversedMessage:function(){
                        //'this' 指向v 实例
                        return this.message.split('').reverse().join('')
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果:

```
原始字符串:Angle

计算机后反转字符串:elgnA
```

提供的函数将用作属性 vm.reversedMessage 的 getter 。

v.reversedMessage 依赖于 v.message，在 v.message 发生改变时，v.reversedMessage 也会更新。

### computed vs methods

可以使用methods来代替computed，效果上两个都是一样的，但是computed是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用methods，在重新渲染的时候，函数总会重新调用执行。

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test22</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test22">
            <p>原始字符串:{{message}}</p>
            <p>计算机后反转字符串:{{reversedMessage}}</p>
            <p>使用方法后反转字符串:{{reversedMessage2()}}</p>

            <script type="text/javascript">
                var v = new Vue({
                    el:"#test22",
                    data:{
                        message:"angle",
                    },
                    methods:{
                        reversedMessage2:function(){
                            return this.message.split('').reverse().join('')
                        }
                    },
                    computed:{
                        reversedMessage:function(){
                            return this.message.split('').reverse().join('')
                        }
                    }
                })
            </script>
        </div>
    </body>
</html>
```

运行结果:

```
原始字符串:angle

计算机后反转字符串:elgna

使用方法后反转字符串:elgna
```

> computed性能更好，但是如果不希望缓存，则可以使用methods属性

### computed setter

computed属性默认只有getter，不过在需要时可以提供一个setter

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test23</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test23">
            <p>{{ site }}</p>
        </div>

        <script>
            var v = new Vue({
                el:"#test23",
                data:{
                    name:"angle",
                    age:"18"
                },
                computed:{
                    site:{
                        //getter
                        get:function(){
                            return this.name + "have" + this.age
                        },
                        //setter
                        set:function(new_value){
                            var names = new_value.split(' ')
                            this.name = names[0]
                            this.age = names[names.length-1]
                        }
                    }
                }
            })

            //调用setter,v.name和v.age 也会相对应被更新
            v.site = 'miku 2000'
            document.write('name:' + v.name)
            document.write("<br />")
            document.write("age:"+v.age)
        </script>
    </body>
</html>
```

运行结果:

```
mikuhave2000

name:miku
age:2000
```

从实例运行结果看在运行`v.site = 'miku 2000';` 时，setter 会被调用， `v.name 和 v.age` 也会被对应更新。

