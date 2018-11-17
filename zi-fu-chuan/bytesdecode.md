### 语法

```
bytes.decode(encoding="utf-8", errors="strict")
```

### 作用

指定的编码格式解码 bytes 对象。默认编码为 'utf-8'

### 参数

* encoding:要使用的编码，如"UTF-8"。

* errors:设置不同错误的处理方案。默认为 'strict',意为编码错误引起一个UnicodeError。 其他可能得值有 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace' 以及通过 codecs.register\_error\(\) 注册的任何值。

### 实例

```
>>> str = "天使"

# 编码
>>> str_utf = str.encode("utf-8")
>>> str_utf
b'\xe5\xa4\xa9\xe4\xbd\xbf'

>>> str_gbk = str.encode("gbk")
>>> str_gbk
b'\xcc\xec\xca\xb9'

# 解码
>>> str_utf.decode('utf-8','strict')
'天使'
>>> str_utf.decode('gbk','strict')
'澶╀娇'
>>> str_gbk.decode('gbk','strict')
'天使'

>>> str_gbk.decode('gbk')
'天使'
>>> str_utf.decode('utf-8')
'天使'
```



