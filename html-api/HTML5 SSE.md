## Server-Sent 事件 - One Way Messaging

Server-Sent 事件指的是网页自动从服务器获得更新。

---

## 接收 Server-Sent 事件通知

EventSource 对象用于接收服务器发送事件通知：

---

## EventSource 对象

在上例中，我们使用 onmessage 事件来获取消息。不过还可以使用其他事件：

| 事件 | 描述 |
| :--- | :--- |
| onopen | 当通往服务器的连接被打开 |
| onmessage | 当接收到消息 |
| onerror | 当发生错误 |



