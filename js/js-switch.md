## JavaScript Switch 语句

请使用 switch 语句来选择要执行的多个代码块之一。

### 语法

```
switch(n)
{
case 1:
  执行代码块 1
  break;
case 2:
  执行代码块 2
  break;
default:
  n 与 case 1 和 case 2 不同时执行的代码
}

```

工作原理：首先设置表达式 n（通常是一个变量）。随后表达式的值会与结构中的每个 case 的值做比较。如果存在匹配，则与该 case 关联的代码块会被执行。请使用_break_来阻止代码自动地向下一个 case 运行。

