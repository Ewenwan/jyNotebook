# 116 Redis的字符串以及过期时间操作

## 连接redis

```text
redis-cli -h 127.0.0.1 -p 6379 或者redis-cli
```

## set语法

```text
set key value [EX seconds] [PX milliseconds]
```

## 设置key-velue

```text
语法:
set key value

示例:
set name angle
```

## 获取value

```text
语法:
get key

示例:
get name
```

注意:如果设置值为多个单词，需要添加双引号

```text
127.0.0.1:6379> set username "hello world"
OK
127.0.0.1:6379> get username
"hello world"
```

## 设置过期时间

#### 如果不设置过期时间，则永久不会过期

### 第一种:

```text
set key value EX seconds
或者
setex key timeout value


# 第一:设置10秒后过期
set name angle EX 10

# 第二:设置3秒后过期
setex name 3 angle
```

### 第二种:

```text
expire key timeout(seconds)
```

## 查看过期时间

```text
语法:
ttl key

示例:
ttl name
```

## 删除数据

```text
语法:
del key

示例:
del name
```

## 删除所有数据

```text
语法:
flushall
```

