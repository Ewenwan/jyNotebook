### v-on指令

事件监听可以使用v-on指令

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test35</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test35">
            <button v-on:click="counter+=1">增加1</button>
            <p>这个按钮被点击了{{counter}}次</p>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test35",
                data:{
                    counter:0
                }
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.10-1.png)

通常情况下，需要使用一个方法来调用JavaScript方法

* v-on可以接收一个定义的方法来调用

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test36</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test36">
            <button v-on:click="greet">greet</button>
        </div>

        <script type="text/javascript">
            var v = new Vue({
                el:"#test36",
                data:{
                    name:"Vue.js",
                },
                //在methods对象中定义方法
                methods:{
                    greet:function(event){
                    //'this' 在方法里指当前vue实例
                    alert("Hello" + this.name + "!");
                    //'event' 是原生DOM事件
                    if(event){
                        alert(event.target.tagName)
                    }
                }
                }
            })

            //也可以用JavaScript直接调用方法
            v.greet()
        </script>
    </body>
</html>
```

* 除了直接绑定，还可以用内联JavaScript语句

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test37</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test37">
            <button v-on:click="say('hi')">Say hi</button>
            <button v-on:click="say('what')">Say what</button>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test37",
                methods:{
                    say:function(message){
                        alert(message)
                    }
                }
            })
        </script>
    </body>
</html>
```

### 事件修饰符

* Vue.js为v-on提供了事件修饰符来处理DOM事件细节，如:event.preventDefault\(\)或event.stopPropagation\(\)

* Vue.js通过由点\(.\)表示的指令后缀来调用修饰符

* .stop

```
 <!-- 阻止单击事件冒泡 -->
 <a v-on:click.stop="doThis"></a>
```

* .prevent

```
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
```

* .capture

```
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">....</div>
```

* .self

```
<!-- 只当事件在元素本身(而不是子元素)触发时触发回调 -->
<div v-on:click.self="doThat">....</div>
```

* .once

```
<!-- click事件只能点击一次 -->
<a v-on:click.once="doThis"></a>
```

### 实例:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>v-on</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
  <style>
    .outer{
      width: 160px;
      height: 160px;
      background: #D45F10;
      border: 1px solid #D45F10;
    }
    .inner{
      width: 100px;
      height: 100px;
      background: #47EE26;
      margin: 30px;
    }
  </style>
</head>
<body>
  <div id="app">

    <h2>.stop阻止事件冒泡</h2>
    <div class="outer" @click="outerClick">
      <div class="inner" @click="innerClick">
        <button @click.stop="btnClick">阻止事件冒泡</button>
      </div>
    </div>
    <p>.stop可以实现当我点击按钮的时候，只触发按钮点击事件，阻止了事件冒泡</p>

  </div>
  <script>
   new Vue({
      el: '#app',
      data: {

      },
      // 在methods中使用data里面的数据的时候，要加this指向该Vue实例对象
      methods: {
        outerClick:function() {
          console.log("触发了outer点击事件")
        },
        innerClick:function() {
          console.log("触发了inner点击事件")
        },
        btnClick:function () {
          console.log("触发了按钮点击事件")
        }
      }
    });
  </script>
</body>
</html>
```

### 按键修饰符

Vue运行在v-on在监听键盘事件时添加按键修饰符

```
<!-- 只有在keyCode是13时调用v.submit() -->
<input v-on:keyup.13="submit />
```

vue为最常用的按键提供了别名

```
<!-- 同上 -->
<input v-on:keyup.enter="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">
```

全部的按键别名:

* `.enter`

* `.tab`

* `.delete`
  \(捕获 "删除" 和 "退格" 键\)
* `.esc`
* `.space`
* `.up`
* `.down`
* `.left`
* `.right`
* `.ctrl`
* `.alt`
* `.shift`
* `.meta`

```
<div id="app">
        <input type="text" id="username" v-on:keyup.enter="submit">
    </div>
    <script type="text/javascript" src="js/vue.js">
    </script>
    <script type="text/javascript">
        new Vue({
            el: '#app',
            methods: {
                submit:function(){
                    alert("试试就试试");
                }
            }
        })
</script>

```



