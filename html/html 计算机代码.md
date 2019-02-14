## HTML 键盘格式

HTML&lt;kbd&gt;元素定义键盘输入

```HTML
    <html>
        <body>
            <p>HTML kbd元素表示键盘输入:</p>
            <p><kbd>File|Open...</kbd></p>
        </body>
    </html>
```

---

## HTML 样本格式

HTML&lt;samp&gt;元素定义计算机输出示例:

```HTML
    <html>
        <body>
            <p>HTML samp 元素表示计算机输出示例</p>
            <samp>
                demo.example.com login: Apr 12 09:10:17 Linux 2.6.10-grsec+gg3+e+fhs6b+nfs+gr0501+++p3+c4a+gr2b-reslog-v6.189
            </samp>
        </body>
    </html>
```

---

## HTML 代码格式

HTML&lt;code&gt;元素定义编程代码示例:

```HTML
       <code>
         #include< iostream >
         using namespace std;
         int main()
         {
           printf("hello world");
           return 0;
         }
       </code>
```

注释:&lt;code&gt;元素不保留多余的空格和折行，所以在浏览器上会去掉多余的空白

提示:需要保留空白，则必须在&lt;pre&gt;&lt;/pre&gt;元素中定义代码

```HTML
<code>
  <pre>
    #include < iostream >
    using namespace std;
    int main()
    {
      printf("hello world");
      return 0;
    }
  </pre>
</code>
```

---

## HTML变量格式化

HTML&lt;var&gt;元素定义数学变量

```HTML
        <p>爱因斯坦的公式:</p>
        <p><var>E</var> = <var>m</var> <var>c</var><sup>2</sup></p>
```

---

## HTML 计算机代码元素

| 标签 | 描述 |
| :--- | :--- |
| &lt;code&gt; | 定义计算机代码文本 |
| &lt;kbd&gt; | 定义键盘文本 |
| &lt;samp&gt; | 定义计算机代码示例 |
| &lt;var&gt; | 定义变量 |
| &lt;pre&gt; | 定义预格式化文本 |



