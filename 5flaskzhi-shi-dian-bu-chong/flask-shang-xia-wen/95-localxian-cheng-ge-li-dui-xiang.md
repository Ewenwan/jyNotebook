# 95 Local线程隔离对象

在'Flask'中，类似于'request'的对象，其实是绑定到了一个'werkzeug.local.Local'对象上。这样即使是同一个对象，那么在多个线程中都是隔离的，类似的对象还有'session'以及'g'对象

Thread Local:只要绑定在Local对象上的属性，在每个线程中都是独立隔离的

实例代码:

```text
from threading import Thread
from werkzeug.local import Local

local = Local()

local.request = '123'

class MyThread(Thread):
    def run(self):
        local.request = 'abc'
        print('子线程',local.request)

mythread = MyThread()
mythread.start()
mythread.join()

print("主线程",local.request)

“”“
子线程 abc
主线程 123
“”“
```

