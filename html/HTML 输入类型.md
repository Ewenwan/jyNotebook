## 输入类型：text

_&lt;input type="text"&gt;_定义供_文本输入_的单行输入字段

---

## 输入类型：password

_&lt;input type="password"&gt;_定义_密码字段_

---

## 输入类型：submit

_&lt;input type="submit"&gt;_定义_提交_表单数据至_表单处理程序_的按钮。

---

## 输入类型: radio

&lt;input type="radio"&gt; 定义单选按钮。

单选按钮允许用户只选择有限数量的选择中的一个

---

## 输入类型: checkbox

&lt;input type="checkbox"&gt; 定义复选框。

复选框允许用户在有限数量的选项中选择零个或多个选项。

---

## 输入类型: button

_&lt;input type="button&gt;_定义_按钮_。

---

## HTML5 输入类型

新增加类型:

* color
* date
* datetime
* datetime-local
* email
* month
* number
* range
* search
* tel
* time
* url
* week

---

## 输入类型：number

_&lt;input type="number"&gt;_用于应该包含数字值的输入字段。

---

## 输入限制

这里列出了一些常用的输入限制（其中一些是 HTML5 中新增的）：

| 属性 | 描述 |
| :--- | :--- |
| disabled | 规定输入字段应该被禁用。 |
| max | 规定输入字段的最大值。 |
| maxlength | 规定输入字段的最大字符数。 |
| min | 规定输入字段的最小值。 |
| pattern | 规定通过其检查输入值的正则表达式。 |
| readonly | 规定输入字段为只读（无法修改）。 |
| required | 规定输入字段是必需的（必需填写）。 |
| size | 规定输入字段的宽度（以字符计）。 |
| step | 规定输入字段的合法数字间隔。 |
| value | 规定输入字段的默认值。 |

---

## 输入类型：date

_&lt;input type="date"&gt;_用于应该包含日期的输入字段。

```
<form>
    日期:
    <input type="date" name="date" />
</form>
```

---

## 输入类型：color

_&lt;input type="color"&gt;_用于应该包含颜色的输入字段。

```HTML
<form>
    选择颜色:
    <input type="color" name="select_color" />
</form>
```

---

## 输入类型：range

_&lt;input type="range"&gt;_用于应该包含一定范围内的值的输入字段。

```HTML
<form>
    <input type="range" name="points" min="0" max="10" />
</form>
```

---

## 输入类型：month

_&lt;input type="month"&gt;_允许用户选择月份和年份。

```
<form>
    日期:
    <input type="month" name="month" />
</form>
```

---

## 输入类型：week

_&lt;input type="week"&gt;_允许用户选择周和年。

```
<form>
    <input type="week" name="select_week" />
</form>
```

---

## 输入类型：time

_&lt;input type="time"&gt;_允许用户选择时间（无时区）。

```
<form>
    <input type="time" name="select_time" />
</form>
```

---

## 输入类型：datetime

_&lt;input type="datetime"&gt;_允许用户选择日期和时间（有时区）。

```
<form>
    <input type="week" name="select_datetime" />
</form>
```

---

## 输入类型：datetime-local

_&lt;input type="datetime-local"&gt;_允许用户选择日期和时间（无时区）。

```
<form>
    <input type="datetime-local" name="select_datetime-local" />
</form>
```

---

## 输入类型：email

_&lt;input type="email"&gt;_用于应该包含电子邮件地址的输入字段。

```
<form>
    <input type="email" name="email" />
</form>
```

---

## 输入类型：search

_&lt;input type="search"&gt;_用于搜索字段（搜索字段的表现类似常规文本字段）。

```
<form>
    <input type="search" name="search" />
</form>
```

---

## 输入类型：tel

_&lt;input type="tel"&gt;_用于应该包含电话号码的输入字段。

```
<form>
    <input type="tel" name="tel" />
</form>
```

---

## 输入类型：url

_&lt;input type="url"&gt;_用于应该包含 URL 地址的输入字段。

```
<form>
    <input type="url" name="url" />
</form>
```



