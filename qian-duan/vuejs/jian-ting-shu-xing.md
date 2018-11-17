### watch

可以同watch来响应数据的变化

实例:通过使用watch实现计数器

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test24</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test24">
            <p style="font-size: 25px;">计数器:{{counter}}</p>
            <button style="font-size: 25px;" @click="counter++">点我</button>
        </div>

        <script type="text/javascript">
            var v = new Vue({
                el:"#test24",
                data:{
                    counter:1
                }
            })
            v.$watch('counter',function(nval,oval){
                alert('计数器值有变化:'+oval+'变为'+nval+'!')
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.8-1.png)

实例2:进行千米和米之间的换算

创建了两个输入框，data 属性中， kilometers 和 meters 初始值都为 0。watch 对象创建了两个方法 kilometers 和 meters

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test25</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test25">
            千米:<input type="text"    v-model="kilometers" />
            米 : <input type="text" v-model="meters" />
        </div>
        <p id="info"></p>

        <script type="text/javascript">
            var v = new Vue({
                el:"#test25",
                data:{
                    kilometers:0,
                    meters:0,
                },
                methods:{

                },
                computed:{

                },
                watch:{
                    kilometers:function(val){
                        this.kilometers = val;
                        this.meters = val * 1000;
                    },
                    meters:function(val){
                        this.kilometers = val / 1000;
                        this.meters = val;
                    },
                },
            })

            //$watch 是一个实例方法
            v.$watch('kilometers',function(newValue,oldValue){
                //这个回调将在v.kilometers 改变后调用
                document.getElementById("info").innerHTML = "修改前值为:" + oldValue + "修改后值为:" + newValue
            })
        </script>
    </body>
</html>
```

运行结果:

![](/assets/1.13.4.8-2.png)

