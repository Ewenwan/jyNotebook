## JavaScript 表单验证

JavaScript 可用来在数据被送往服务器前对 HTML 表单中的这些输入数据进行验证。

被 JavaScript 验证的这些典型的表单数据有：

* 用户是否已填写表单中的必填项目？
* 用户输入的邮件地址是否合法？
* 用户是否已输入合法的日期？
* 用户是否在数据域 \(numeric field\) 中输入了文本？



## 必填（或必选）项目

下面的函数用来检查用户是否已填写表单中的必填（或必选）项目。假如必填或必选项为空，那么警告框会弹出，并且函数的返回值为 false，否则函数的返回值则为 true（意味着数据没有问题）：

```
function validate_required(field,alerttxt)
{
with (field)
{
if (value==null||value=="")
  {alert(alerttxt);return false}
else {return true}
}
}
```





## E-mail 验证

下面的函数检查输入的数据是否符合电子邮件地址的基本语法。

意思就是说，输入的数据必须包含 @ 符号和点号\(.\)。同时，@ 不可以是邮件地址的首字符，并且 @ 之后需有至少一个点号：

```
function validate_email(field,alerttxt)
{
with (field)
{
apos=value.indexOf("@")
dotpos=value.lastIndexOf(".")
if (apos
<
1||dotpos-apos
<
2) 
  {alert(alerttxt);return false}
else {return true}
}
}
```



