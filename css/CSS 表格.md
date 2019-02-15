## 表格边框

设置表格边框，使用border属性

实例:表格具有双线条边框

```HTML
table,th,td{
    border:1px solid black;
}
```

---

## 折叠边框

boder-collapse属性设置是否将表格边框折叠为单一边框

可选值:

separate\(\):默认。边框会被分开

collapse:边框合并为一个单一的边框

```HTML
table{
    border-collapse:collapse;
}
table,th,td{
    border:1px solid black;
]
```

---

## 表格宽度和高度

通过width和height属性定义表格的宽度和高度

```HTML
table{
    width:100%;
}
th{
    height:50px;
}
```

---

## 表格文本对齐

text-align和vertical-align（vertical垂直的、align排列）

text-align属性设置水平对齐方式

```HTML
td{
    text-align:right;
}
```

vertical-align属性设置垂直对齐方式

```HTML
td{
    height:50px;
    vertical-align:bottom;
}
```

---

## 表格内边距

padding属性控制表格中内容与边框的距离

```HTML
<html>
    <head>
        <style>
            table,th,td{
                border:1px solid black;
            }

            td{
                padding:50px;
                //padding:10px;
            }
        </style>
    </head>
    <body>
        <table>
            <tr>
                <th>first</th>
            </tr>
            <tr>
                <td>one</td>
            </tr>
            <tr>
                <td>tow</td>
            </tr>
        </table>
    </body>
</html>
```

---

## 表格颜色

实例:设置边框的颜色、以及th元素的文本和背景颜色

```HTML
table,td,th{
    boder:1px soild green;
}

th{
    background-color:green;
    color:white;
}
```

color:设置文本颜色

background-color:背景色

---

## border-spacing属性

border-spacing属性设置相邻丹阳的边框间的距离\(仅用于边框分离模式\)

可选值:

length:规定相邻单元的边框之间的距离。使用 px、cm 等单位。不允许使用负值。

如果定义一个length参数，那么定义的是水平和垂直间距。

如果定义两个length参数，那么第一个设置水平间距，而第二个设置垂直间距。

---

## caption-side属性

caption-side属性设置表格标题的位置

可选值:

top:默认值。把表格标题定位在表格之上

bottom:把表格标题定位在表格之下

实例:把标题置于表格下方

```
caption{
    caption-side:bottom;
}
```

---

## empty-cells属性

empty-cells属性设置是否显示表格中的空单元格\(仅用于"分离边框"模式\)

可选值:

hide:不在空单元格周围绘制边框

show:在空单元格周围绘制边框

```HTML
table{
    border-collapse:separate;
    empty-cells:hide;
}
```

---

## table-layout属性

tablelayout属性用来显示表格单元格、行、列的算法规则

可选值:

automatic:默认。列宽度由单元格内容设定

fixed:列宽由表格宽度和列宽度设定

```HTML
table{
    table-layout:fixed;
}
```

---

_实例:_

#### 漂亮的表格

```HTML
<html>
  <head>
    <style type="text/css">
    #customers
      {
        font-family:"Trebuchet MS", Arial, Helvetica, sans-serif;
        width:100%;
        border-collapse:collapse;
      }

    #customers td, #customers th 
      {
        font-size:1em;
        border:1px solid #98bf21;
        padding:3px 7px 2px 7px;
      }

    #customers th 
      {
        font-size:1.1em;
        text-align:left;
        padding-top:5px;
        padding-bottom:4px;
        background-color:#A7C942;
        color:#ffffff;
      }

    #customers tr.alt td 
      {
        color:#000000;
        background-color:#EAF2D3;
      }
    </style>
  </head>

  <body>
    <table id="customers">
      <tr>
        <th>Company</th>
        <th>Contact</th>
        <th>Country</th>
      </tr>

      <tr>
        <td>Apple</td>
        <td>Steven Jobs</td>
        <td>USA</td>
      </tr>

      <tr class="alt">
      <td>Baidu</td>
      <td>Li YanHong</td>
      <td>China</td>
      </tr>

      <tr>
        <td>Google</td>
        <td>Larry Page</td>
        <td>USA</td>
      </tr>

      <tr class="alt">
        <td>Lenovo</td>
        <td>Liu Chuanzhi</td>
        <td>China</td>
      </tr>

      <tr>
        <td>Microsoft</td>
        <td>Bill Gates</td>
        <td>USA</td>
      </tr>

      <tr class="alt">
        <td>Nokia</td>
        <td>Stephen Elop</td>
        <td>Finland</td>
      </tr>
    </table>
  </body>
</html>
```



