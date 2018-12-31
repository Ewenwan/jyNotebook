Application对象的语法:

```
Application["变量名"] = "变量值"
```

---

## Application对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| All | 获取全部的Application对象变量 |
| AllKeys | 获取全部的Application对象变量名称 |
| Count | 获取Application对象变量的数量 |

---

## Application对象的常用方法

| 属性 | 说明 |
| :--- | :--- |
| Add | 添加新的Application对象变量 |
| Clear | 清除所有Application对象变量 |
| Get | 通过索引获取变量值 |
| GetKey | 通过索引获取变量名称 |
| Lock | 锁定Application对象变量 |
| Remove | 移除Application对象变量 |
| RemoveAll | 移除所有Application对象变量 |
| set | 更新application对象变量的值 |
| Unlock | 解除对application对象的锁定 |

```
Application.Add('name','angle')
'通过索引获取'
Application.Get(0)
Application.GetKey(0)
```



