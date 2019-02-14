window.screen对象包含有关的用户屏幕的信息

## window Screen

window.screen 对象在编写时可以不使用window这个前缀

一些属性:

* screen.availWidth - 可用的屏幕宽度
* screen.availHeight - 可用的屏幕高度

---

## Window Screen可用宽度

screen.availWidth属性返回访问者屏幕的宽度，以像素计，减去界面特性，比如窗口任务栏

实例:返回屏幕的可用宽度:

```
<script>
    document.write("可用宽度:"+screen.availWidth);
</script>
```

---

## Window Screen 可用高度

screen.availHeight 属性返回访问者屏幕的高度，以像素计，减去界面特性，比如窗口任务栏

实例:返回屏幕的可用高度

```
<script>
    document.write("可用高度:"+screen,availHeight)
</script>
```



