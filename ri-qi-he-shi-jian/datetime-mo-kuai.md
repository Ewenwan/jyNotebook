### datetime模块

```
import datetime
1.返回当前时间
>>> datetime.datetime.now()
datetime.datetime(2018, 10, 11, 17, 4, 59, 425069)

2.时间戳转换成日期
>>> datetime.date.fromtimestamp(1178766678)
datetime.date(2007, 5, 10)

3.当前时间+3天
>>> datetime.datetime.now() + datetime.timedelta(+3)
datetime.datetime(2018, 10, 14, 17, 5, 9, 143665)

4.当前时间-3天
>>> datetime.datetime.now() + datetime.timedelta(-3)
datetime.datetime(2018, 10, 8, 17, 5, 18, 367217)

5.当前时间+3小时
>>> datetime.datetime.now() + datetime.timedelta(hours=3)
datetime.datetime(2018, 10, 11, 20, 5, 34, 853441)

6.当前时间+30分钟
>>> datetime.datetime.now() + datetime.timedelta(minutes=30)
datetime.datetime(2018, 10, 11, 17, 35, 44, 278555)

7.  年，月，日，时，分，秒，毫秒
>>> now = datetime.datetime.now()
>>> now
datetime.datetime(2018, 10, 11, 16, 52, 22, 444832)
>>> now.year
2018
>>> now.month
10
>>> now.day
11
>>> now.hour
16
>>> now.minute
52
>>> now.second
22
>>> now.microsecond
444832
>>>
```



