混入 \(mixins\)定义了一部分可复用的方法或者计算属性。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。

实例:

```
<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title>test59</title>
        <script src="https://cdn.staticfile.org/vue/2.4.2/vue.js"></script>
    </head>

    <body>
        <div id="test59"></div>
        <script>
            var v = new Vue({
                el: "#test59",
                data: {

                },
                methods: {

                }
            })

            //定义一个混入对象
            var myMixin = {
                created: function() {
                    this.startmixin()
                },
                methods: {
                    startmixin: function() {
                        document.write("欢迎来到混入实例")
                    }
                }
            }

            var Component = Vue.extend({
                mixins: [myMixin]
            })

            var component = new Component()
        </script>
    </body>

</html>
```

运行结果

```
欢迎来到混入实例
```

### 选项合并

当组件和混入对象含有同名选项时，这些选项将以恰当的方式混合

比如，数据对象在内部会进行浅合并 \(一层属性深度\)，在和组件的数据发生冲突时以组件数据优先

实例:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test60</title>
        <script src="https://cdn.staticfile.org/vue/2.4.2/vue.js"></script>
    </head>
    <body>
        <div id="test60"></div>
        <script>
            var mixin = {
                created:function(){
                    document.write("混入调用" + "<br />")
                }
            }

            new Vue({
//                el:"#test60",
                mixins:[mixin],
                created:function(){
                    document.write("组件调用" + "<br/>")
                }
            })
        </script>
    </body>
</html>
```

```
混入调用
组件调用
```

如果 methods 选项中有相同的函数名，则 Vue 实例优先级会较高。如下实例，Vue 实例与混入对象的 methods 选项都包含了相同的函数：

```
<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title>test60</title>
        <script src="https://cdn.staticfile.org/vue/2.4.2/vue.js"></script>
    </head>

    <body>
        <div id="test60"></div>
        <script>
            var mixin = {
                methods: {
                    created: function() {
                        document.write("created方法" + "<br />")
                    },
                    samemethod: function() {
                        document.write("Mixin:相同方法名" + "<br />")
                    }
                }
            }

            var v = new Vue({
                mixins: [mixin],
                methods: {
                    start: function() {
                        document.write("start方法" + "<br/>")
                    },
                    samemethod: function() {
                        document.write("Main:相同方法名" + "<br />")
                    }
                }
            })

            v.created();
            v.start();
            v.samemethod();
        </script>
    </body>

</html>
```

```
created方法
start方法
Main:相同方法名
```

从输出结果 methods 选项中如果碰到相同的函数名则 Vue 实例有更高的优先级会执行输出

### 全局混入

也可以全局注册混入对象。注意使用！ 一旦使用全局混入对象，将会影响到 所有 之后创建的 Vue 实例。使用恰当时，可以为自定义对象注入处理逻辑。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
<body>
<script type = "text/javascript">
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      document.write(myOption)
    }
  }
})

new Vue({
  myOption: 'hello!'
})
// => "hello!"
</script>
</body>
</html>
```



