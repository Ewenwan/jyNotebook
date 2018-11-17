现在开始讲解如何处理时间，这里处理时间的模块只讲解time模块和datetime模块

### 了解

UTC（Coordinated Universal Time）即格林威治天文时间，为世界标准时间。中国北京为UTC+8。  
 DST（Daylight Saving Time）即夏令时。  
 时间戳（timestamp）的方式：通常来说，时间戳是指格林威治时间1970年01月01日00时00分00秒\(北京时间1970年01月01日08时00分00秒\)起至现在的总秒数。

我们运行“type\(time.time\(\)\)”，返回的是float类型。  
 返回时间戳方式的函数主要有time\(\)，clock\(\)等。  
 元组（struct\_time）方式：struct\_time元组共有9个元素，返回struct\_time的函数主要有gmtime\(\)，localtime\(\)，strptime\(\)

