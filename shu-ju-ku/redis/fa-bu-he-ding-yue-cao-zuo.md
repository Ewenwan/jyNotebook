**给某个频道发布消息**

```text
语法:
publish channel message

示例:
# 向channe2拼单发送消息hello
127.0.0.1:6379> publish channe2 hello
(integer) 1
127.0.0.1:6379>
```

* **订阅某个频道的消息**

```text
语法:
subscribe channel[channel...]

示例:
# 订阅channe2频道，如果channe2频道发布消息，则会将消息显示出来
127.0.0.1:6379> subscribe channe2
subscribe
channe2
1
message
channe2
hello
```



