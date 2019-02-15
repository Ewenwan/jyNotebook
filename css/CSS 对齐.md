## 对齐块元素对齐

块元素指的是占据全部可用宽度的元素，并且在其前后都会换行

比如:&lt;h1&gt;、&lt;p&gt;、&lt;div&gt;

---

## 使用margin属性来水平对齐

可通过将左和右外边距设置为"auto"，来对齐块元素

```
<html>
    <head>
        <style>
            .center{
                //margin-left:auto;
                //margin-right:auto;
                margin:auto;
                background-color:red;
            }
        </style>
    </head>
    <body>
        <div class="center">
            <p>angle</p>
        </div>
    </body>
</html>
```

_tips:记住要声明&lt;!doctype html&gt;_

---

## 使用position属性进行左和右对齐

对齐元素的方法之一是使用绝对定位

```
.right{
    position:absolute;
    right:0px;
    width:300px;
    background-color:#b0e0e6;
}
```

---

## 使用float属性来进行左和右对齐

对齐元素的另一种方法是使用float属性

```
.right{
    float:right;
    width:300px;
    background-color:red;
}
```



