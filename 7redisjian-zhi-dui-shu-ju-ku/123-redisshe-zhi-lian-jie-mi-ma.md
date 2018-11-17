# 123 Redis设置连接密码

## 设置redis密码

在windows中，配置文件为redis.windows-service.conf

在Ubuntu中，配置文件为redis.conf

将配置文件中的"requirepass password"取消注释，设置密码

```text
requirepass 123456
```

临时设置密码，但是重启服务后失效

```text
config set requirepass password
config get requirepass
auth overload
```

## 连接redis

```text
有两种方式:

redis-cli -h 127.0.0.1 -p 6379 -a 123456

或者

redis-cli -h 127.0.0.1 -p 6379
> auth 123456
```

