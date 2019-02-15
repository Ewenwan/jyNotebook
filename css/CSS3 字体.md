## @font-face

导入新的字体

实例:

```
@font-face
{
    font-family:myFirstFont;
    src:url("新字体的存放路径");
}
```

## 使用粗体字体

为粗体文本添加另一个包含描述符的@font-face

```
@font-face
{
    font-family:myFirstFont;
    src:url("新的存放字体的路径");
    font-weight:bold;
}
```

## CSS3 字体描述符

下面的表格列出了能够在 @font-face 规则中定义的所有字体描述符：

| 描述符 | 值 | 描述 |
| :--- | :--- | :--- |
| font-family | name | 必需。规定字体的名称。 |
| src | URL | 必需。定义字体文件的 URL。 |
| font-stretch | normalcondensedultra-condensedextra-condensedsemi-condensedexpandedsemi-expandedextra-expandedultra-expanded | 可选。定义如何拉伸字体。默认是 "normal"。 |
| font-style | ormalitalicoblique | 可选。定义字体的样式。默认是 "normal"。 |
| font-weight | normalbold100200300400500600700800900 | 可选。定义字体的粗细。默认是 "normal"。 |
| unicode-range | unicode-range | 可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。 |



