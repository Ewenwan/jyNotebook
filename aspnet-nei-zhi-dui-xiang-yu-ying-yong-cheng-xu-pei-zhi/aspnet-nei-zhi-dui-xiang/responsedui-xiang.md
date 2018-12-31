## Response对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| Bffuer | 表名页面输出是否启用缓存 |
| Cache | 获取网页的缓存策略 |
| Charset | 获取或设置输出流的HTTP字符集 |
| Expires | 获取或设置在浏览器上缓存的页面超时的时间 |
| IsClienConnected | 指定客户端是否连接在服务器上 |
| Status | 服务器返回的状态行的值 |

---

### _Response_对象主要用于动态地响应客户端请求，并将结果返回到客户端浏览器中

---

## Response对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| AddHeader | 设置HTML的标题 |
| BinaryWrite | 以二进制字符串方式向客户端输出数据 |
| Clear | 当Buffer属性值为True时，清空缓冲区所有的内容 |
| End | 当缓冲的输出发到客户端，停止运行当前页面 |
| Flush | 当Buffer属性值为True时，向客户端输出所有缓冲的内容 |
| Output | 把文本输出到客户端 |
| OutputStream | 把二进制流输出到客户端 |
| Redirect | 将客户端重定向到指定的URL |
| write | 把字符数组写入到HTTP响应输出流 |
| writeFile | 把文件输出写入HTTP响应输出流 |
| Redirect | 重定向到某一页面 |

---

## Response.aspx页面中的控件

| 控件类型 | 空间名称\(ID\) | 作用 |
| :--- | :--- | :--- |
| Label | Label1 | 显示用户名标签 |
| Label | Label2 | 显示密码标签 |
| TextBox | TextUsername | 输入用户名 |
| TextBox | TextPassword | 输入密码 |
| Button | BtnLogin | 确认登录 |

---

注意:

```
protected void Page_Load(...)  '当页面加载时触发'
```



