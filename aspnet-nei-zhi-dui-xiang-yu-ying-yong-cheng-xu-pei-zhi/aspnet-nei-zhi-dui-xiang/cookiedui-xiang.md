设置Cookie的方法

```
Response.Cookies['名称'].value = "值"
```

---

## Cookie对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| Count | 获取Cookies中Cookie的数量 |
| Domain | 获取或设置Cookie的域 |
| Name | 获取或设置Cookie的名称 |
| Value | 获取或设置Cookie的值 |
| Expires | 获取或设置Cookie的过期时间 |

---

## Cookie对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| Add | 增加一个Cookie变量 |
| Clear | 删除所有Cookie变量 |
| Get | 通过名称获取一个Cookie变量的值 |
| GetKey | 通过索引获取一个Cookie变量的值 |
| Remove | 移除一个Cookie变量 |

```
Response.Cookie['名称'].Expires 设置/获取cookie的过期时间
```



