_tips:javascript的所有事物都是对象:字符串，数字，数组，日期，等等_

在javascript中，对象是拥有属性和方法的数据**JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...**

**此外，JavaScript 允许自定义对象。**

---

## 创建javascript对象

创建新对象两种不同的方法

* 定义并创建对象的实例
* 使用函数来定义对象，然后创建新的对象实例

---

## 创建直接的实例

创建对象的一个新实例，并添加几个属性

```
person = new Object();
person.firstname = "Bill"
person.lastname = "Gates"
person.age = 56
person.eyecolor = "blue"
```

```
person={firstname:"John",lastname:"Doe",age:50,eyecolor:"blue"};
```

---

## 使用对象构造器

```
funtion person(firstname,lastname,age,eyecolor)
{
    this.firstname = firstname;
    this.lastname = lastname;
    this.age = age;
    this.eyecolor = eyecolor;
}
```

---

## 把方法添加到 JavaScript 对象

方法只不过是附加在对象上的函数。

在构造器函数内部定义对象的方法：

```
<!DOCTYPE html>
<html>
<body>
<script>
function person(firstname,lastname,age,eyecolor)
{
this.firstname=firstname;
this.lastname=lastname;
this.age=age;
this.eyecolor=eyecolor;

this.changeName=changeName;
function changeName(name)
{
this.lastname=name;
}
}
myMother=new person("Steve","Jobs",56,"green");
myMother.changeName("Ballmer");
document.write(myMother.lastname);
</script>

</body>
</html>
```

changeName\(\) 函数 name 的值赋给 person 的 lastname 属性。

现在您可以试一下：

```
myMother.changeName("Ballmer");
```

---

## JavaScript for...in 循环

JavaScript for...in 语句循环遍历对象的属性。

和python一样

### 语法

```
for (对象中的变量)
  {
  要执行的代码
  }
```



