## javascript window location

window.location 对象用于获得当前页面的地址\(URL\),并把浏览器重定向到新的页面

---

## window Location

一些例子:

* location.hostname 返回web主机的域名
* location.pathname 返回当前页面的路径和文件名
* location.port 返回web主机的端口\(80/443\)
* location.protrol 返回所使用的web协议\([http://或https//\](http://或https//\)\)

---

## Window Location Href

location.href 属性返回当前页面的URL

实例:返回\(当前页面的\)整个URL

```
<script>
    document.write(location.href)
</script>
```

---

## Window Location Pathname

location.pathname 属性返回url的路径名

实例:返回当前url的路径名

```
<script>
    document.write(location.pathname);
</script>
```

---

## Window Location Assign

location.assign\(\)方法加载新的文档

assign\(分配\)

```
<!DOCTYPE HTML>
<html>
    <head>
        <script>
            function newDoc()
            {
                window.location.assign("http://www.w3school.com.cn");
            }
        </script>
    </head>
    <button type="button" onclick="newDoc()" value="加载新文档"></button>
</html>
```



