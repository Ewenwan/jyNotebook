### 语法

```
ascii(object)
```

### 作用

ascii\(\) 函数类似 repr\(\) 函数, 返回一个表示对象的字符串, 但是对于字符串中的非 ASCII 字符则返回通过 repr\(\) 函数使用 \x, \u 或 \U 编码的字符

### 参数

* object:对象

### 实例

```
>>> ascii("adasd")
"'adasd'"
```



