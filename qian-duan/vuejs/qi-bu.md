### Vue.js起步

每个应用都需要通过实例化Vue来实现

##### 语法

```
var v = new Vue({

})
```

##### 实例

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Demo2</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test">
            <h1>site:{{site}}</h1>
            <h1>url:{{url}}</h1>
            <h1>{{details()}}</h1>
        </div>

        <script type="text/javascript">
            var t = new Vue({
                el:'#test',
                data:{
                    site:"天使",
                    url:"www.python.org",
                },
                methods:{
                    details:function(){
                        return this.site + "为了梦想，一直向上";
                    }
                }
            })
        </script>

    </body>
</html>
```

运行结果

![](/assets/1.13.4.3-1.png)

可以看到在Vue构造器中有一个el参数，是Dom元素中的id，在上面实例中为test，在div元素中

```
<div id="test"></div>
```

这代表这接下来的改动全部在以上的指定的div内，div外部不受影响

##### 如何定义数据对象

* `data`:用于定义属性，实例中有三个属性分别为:site，url，alexa
* `methods`:用于定义的函数，可以通过return来返回函数
* `\{\{\}\}`:用于输出对象属性和函数返回值

```
<div id="test">
    <h1>site:{{site}}</h1>
    <h1>url:{{url}}</h1>
    <h1>{{details()}}</h1>
</div>
```

当一个 Vue 实例被创建时，它向 Vue 的响应式系统中加入了其 data 对象中能找到的所有的属性。当这些属性的值发生改变时，html 视图将也会产生相应的变化。

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Vue 测试实例</title>
    <script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
<body>
    <div id="vue_det">
        <h1>site : {{site}}</h1>
        <h1>url : {{url}}</h1>
        <h1>Alexa : {{alexa}}</h1>
    </div>
    <script type="text/javascript">
    // 我们的数据对象
    var data = { site: "python", url: "www.python.org", alexa: 10000}
    var vm = new Vue({
        el: '#vue_det',
        data: data
    })
    // 它们引用相同的对象！
    document.write(vm.site === data.site) // true
    document.write("<br>")
    // 设置属性也会影响到原始数据
    vm.site = "Runoob"
    document.write(data.site + "<br>") // Runoob

    // ……反之亦然
    data.alexa = 1234
    document.write(vm.alexa) // 1234
    </script>
</body>
</html>
```

除了属性属性，Vue实例还提供了一些有用的实例属性与方法，都有前缀$，以便与用户定义的属性区分开来。

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>test2</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test2">
            <h1>site:{{site}}</h1>
            <h1>url:{{url}}</h1>
            <h1>alexa:{{alexa}}</h1>
        </div>

        <script type="text/javascript">
            var data = { site: "天使", url: "www.python.org", alexa: 10000}
            var v = new Vue({
                el:'#test2',
                data:data
            })

            document.write(v.$data === data) // true
            document.write("<br />")
            document.write(v.$el === document.getElementById("test2"))
        </script>

    </body>
</html>
```

运行结果

![](/assets/1.13.4.3-2.png)

```
var v = new Vue({

})

document.write(v.$data === data) // true
```



