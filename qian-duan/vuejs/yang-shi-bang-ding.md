### Vue.js class

class与style是HTML元素的属性，用于设置元素的样式，可以用v-bind来设置样式属性

Vue.js v-bind在处理class 和 style 时，专门增强了它，表达式的结果类型除了字符串之外，还可以是对象或数组。

### class 属性绑定

* 可以为v-bind:class 设置一个对象，从而动态的切换class

实例1:实例中将isActive设置为true显示了一个绿色的div块，如果设置为false则不显示

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test26</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .active {
                width: 100px;
                height: 100px;
                background: green;
            }
        </style>
    </head>
    <body>
        <div id="test26">
            <div v-bind:class="{active:isActive}"></div>
        </div>
        <script type="text/javascript">
            new Vue({
                el:"#test26",
                data:{
                    isActive:true,
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.9-2.png)

等价与

```
<div class="avtice"></div>
```

实例2:text-danger类背景颜色覆盖了active类的背景色

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test27</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .active{
                width:100px;
                height:100px;
                background-color: green;
            }
            .text-danger{
                background:red;
            }
        </style>
    </head>
    <body>
        <div id="test27">
            <div class="static" v-bind:class="{active:isActive,'text-danger':hasError}"></div>
        </div>

        <script>
            new Vue({
                el:"#test27",
                data:{
                    isActive:true,
                    hasError:true,
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.9-1.png)

等价与

```
<div class="static active text-danger"></div>
```

* 直接绑定数据里的一个对象

实例3:text-danger类背景色覆盖了active类的背景色

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test28</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .active{
                width:100px;
                height:100px;
                background-color: green;
            }
            .text-danger{
                background:red;
            }
        </style>
    </head>
    <body>
        <div id="test28">
            <div class="static" v-bind:class="classObject"></div>
        </div>

        <script>
            new Vue({
                el:"#test28",
                data:{
                    classObject:{
                        active:true,
                        'text-danger':true,
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果和上图一致

* 可以绑定返回对象的计算属性\(这是一个常用且强大的模式\)

实例4:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test29</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .active{
                width:100px;
                height: 100px;
                background-color: green;
            }
            .text-danger{
                width:100px;
                height: 100px;
                background-color: red;
            }
        </style>
    </head>
    <body>
        <div id="test29">
            <div v-bind:class="classObject"></div>
        </div>

        <script>
            new Vue({
                el:"#test29",
                data:{
                    isActive:true,
                    error:null,

                },
                computed:{
                    classObject:function(){
                        return {
                            active:this.isActive && !this.error,
                            'text-danger':this.error && this.error.type === 'fatal'
                        }
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.9-3.png)

### 数组语法

* 可以把一个数组传给v-bind:class

实例5:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test30</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .active{
                width:100px;
                height:100px;
                background:green;
            }

            .text-danger{
                background-color:red;
            }
        </style>
    </head>
    <body>
        <div id="test30">
            <div v-bind:class="[activeClass,errorClass]"></div>
        </div>

        <script type="text/javascript">
            new Vue({
            el:"#test30",
            data:{
                activeClass: 'active',
                errorClass: 'text-danger'
            }
            })
        </script>
    </body>
</html>
```

等价于

```
<div class="active text-danger"></div>
```

* 可以使用三元表达式来切换列表中的class

实例6:errorClass是始终存在的，isActive为true时添加activeClass类

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test30</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
        <style>
            .text-danger {
                width: 100px;
                height: 100px;
                background: red;
            }
            .active {
                width: 100px;
                height: 100px;
                background: green;
            }
        </style>
    </head>
    <body>
        <div id="test30">
            <!--<div v-bind:class="[activeClass,errorClass]"></div>-->
            <div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test30",
                data:{
                    isActive:true,
                    activeClass: 'active',
                    errorClass: 'text-danger'
                }
            })
        </script>
    </body>
</html>
```

> 注意text-danger和active的样式顺序，如果两个位置顺序调换则一直显示红色

### Vue.js stye\(内联样式\)

语法：`<div v-bind:style="{ color: 'red', 'font-size': '50px' }">Angle</div>`

对象内的关键字与普通`css`样式对应，同时也可以是`驼峰式`写法，比如上面的可以写成：`{color: 'red', fontSize: '50px'}`

* 在v-bind:style直接设置样式

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test31</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    <style>
    </style>
    </head>
    <body>
        <div id="test31">
            <!--<div v-bind:style="{color:activeColor,fontSize:fontSize+'px'}">Angle</div>-->
            <div v-bind:style="{ color: 'red', 'font-size': '50px' }">Angle</div>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test31",
                data:{
                    activeColor:"green",
                    fontSize:50
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.9-4.png)

等价于:

```
<div style="color: green; font-size: 50px;">Angle</div>
```

* 直接绑定到一个样式对象，让模板更加清晰

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test32</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test32">
            <div v-bind:style="styleObject">Angle</div>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test32",
                data:{
                    styleObject:{
                        color:"green",
                        fontSize:"50px",
                    }
                }
            })
        </script>
    </body>
</html>
```

* v-bind:style 可以使用数组将多个样式对象应用到一个元素上

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test33</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test33">
            <div v-bind:style="[baseStyles,overridingStyles]">Angle</div>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test33",
                data:{
                    baseStyles:{
                        color:"green",
                        fontSize:"30px",
                    },
                    overridingStyles:{
                        fontSize:"50px",
                        'font-weight':'bold'
                    }
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.9-5.png)

`注意：当 v-bind:style 使用需要特定前缀的 CSS 属性时，如 transform ，Vue.js 会自动侦测并添加相应的前缀。`





