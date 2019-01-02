```
$(document).ready(function(){
    $('.wp').click(function(){
//        $(this).text(jsonArray[0].username)
    $.each(jsonArray,function(index,json){
        $.each(json,function(name,value){
            $(".wp").append("<option value=" + name + ">" + value + "</option>")
        })
        })
    })

})
```

* 使用$.each\(object,function\(index,object\)\)进行循环遍历
  * 字典为键值对
  * 列表为下标和对像



