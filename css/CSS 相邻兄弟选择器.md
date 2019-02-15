## 相邻选择器

相邻选择器，通过加号\(+\)分隔符进行定义。其基本结构是第一个选择器指定前面相邻元素，后面的选择器指定相邻元素。

注意:前后选择符的关系是兄弟关系，即在HTML结构中，两个标签前为兄后为第，否则样式无法应用

```
<!document html>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            h2,p,h3{
                margin:0;
                padding:0;
                height:20px;
            }
            p+h3{
                background-color:pink;
            }
        </style>
    </head>
    <body>
        <p>angle</p>
        <h3>one angle</h3>
        <h2>------</h2>
        <h3>tow angle</p>
        <h2>angle</h2>
        <h3angle></h3>
        <p>angle</p>
    </body>
</html>
```

## 兄弟选择器

通过波浪号\(~\)分隔符进行定义。其基本结构是第一个选择器指定同级前置元素，后面的选择器指定其后同级所有匹配元素。前后选择符的关系是兄弟关系，即在HTML结构中两个标签前为兄后为弟，否则样式无法使用

tips:兄弟选择器能够选择前置元素后同级的所有匹配元素，而相邻选择器只能选择前置元素后相邻的一个匹配元素

```
<!document html>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            h2,p,h3{
                margin:0;
                padding:0;
                height:20px;
            }
            p+h3{
                background-color:pink;
            }
        </style>
    </head>
    <body>
        <p>angle</p>
        <h3>one angle</h3>
        <h2>------</h2>
        <h3>tow angle</p>
        <h2>angle</h2>
        <h3angle></h3>
        <p>angle</p>
    </body>
</html>
```



