## 数值型不同类型数据的转换

#### 1.自动类型转换

不同类型进行运算时，转换时的优先级

低-&gt;byte-&gt;short-&gt;char-&gt;int-&gt;long-&gt;float-&gt;double-&gt;高

#### 2.强制类型转换

强制类型转换的格式

```
(强制转换的类型) 变量名
```

---

## 字符串型数据与整型数据相互转换

#### 1.字符串转换成数值型数据

字符串转换成数值型数据的方法

| 转换的方法 | 功能说明 |
| :--- | :--- |
| Byte.parseByte\(String s\) | 将数字字符串转换成字节型数据 |
| Short.parseShort\(String s\) | 将数字字符串转换为短整型数据 |
| Integer.parseInt\(String s\) | 将数字字符串转换为整型数据 |
| Long.parseLong\(String s\) | 将数字字符串转换为长整型数据 |
| Float.parsetFloat\(String s\) | 将数字字符串转换为浮点型数据 |
| Double.parseDouble\(String s\) | 将数字字符串转换为双精度型数据 |
| Boolean.parseBoolean\(String s\) | 将字符串转换为布尔型数据 |

---

#### 2.数值型数据转换成字符串

```
例如:
int a = 1;//定义变量a
String b = "" + a;//将整型数据转换成了字符串
```



