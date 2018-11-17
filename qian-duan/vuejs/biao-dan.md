* 可以用 v-model 指令在表单控件元素上创建双向数据绑定

v-model 会根据控件类型自动选取正确的方法来更新元素

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test39</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test39">
            <p>input元素:</p>
            <input v-model="message" placeholder="编辑" />
            <p>消息是:{{message}}</p>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test39",
                data:{
                    message:""
                }
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.11-1.png)

### 复选框

* 复选框的双向数据绑定

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test40</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test40">
            <p>单个复选框</p>
            <input type="checkbox" id="a" value="a" v-model="check" />
            <label for="checkbox">{{check}}</label>

            <p>多个复选框</p>
            <input type="checkbox" id="a" value="a" v-model="check2" />
            <label for="a">a</label>

            <input type="checkbox" id="b" value="b" v-model="check2" />
            <label for="b">b</label>

            <input type="checkbox" id="c" value="c" v-model="check2" />
            <label for="c">c</label>

            <input type="checkbox" id="" value="d" v-model="check2" />
            <label for="d">d</label>
            <br />
            <span>选择的值为:{{check2}}</span>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test40",
                data:{
                    check:false,
                    check2:[]
                }
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.11-2.png)

### 单选按钮

* 单选按钮的双向数据绑定

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test41</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test41">
            <input type="radio" id="a" value="angle" v-model="picked"/>
            <label for="a">angle</label>
            <input type="radio" id="m" value="miku" v-model="picked"/>
            <label for="m">miku</label>
            <br  />
            <span>选中的值为:{{ picked }}</span>
        </div>
        <script type="text/javascript">

            var name = document.getElementById("a").value;

            var v = new Vue({
                el:"#test41",
                data:{
                    picked:"",
                }
            })

            v.picked = name;
        </script>
    </body>
</html>
```

![](/assets/1.13.4.11-3.png)

### select列表

* 下拉列表的双向数据绑定

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>test42</title>
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
    </head>
    <body>
        <div id="test42">
            <select v-model="selected" name="fruit">
                <option value="?">选择水果</option>
                <option value="apple">苹果</option>
                <option value="banana">香蕉</option>
            </select>

            <div id="output">
                选择的水果是:{{selected}}
            </div>
        </div>

        <script type="text/javascript">
            new Vue({
                el:"#test42",
                data:{
                    selected:"?"
                }
            })
        </script>
    </body>
</html>
```

![](/assets/1.13.4.11-5.png)

## 修饰符

### .lazy

在默认情况下， v-model 在 input 事件中同步输入框的值与数据，但你可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步：

```
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model.lazy="msg" >
```

### .number

如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值：

```
<input v-model.number="age" type="number">
```

这通常很有用，因为在 type="number" 时 HTML 中输入的值也总是会返回字符串类型。

### .trim

如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入：

```
<input v-model.trim="msg">
```





