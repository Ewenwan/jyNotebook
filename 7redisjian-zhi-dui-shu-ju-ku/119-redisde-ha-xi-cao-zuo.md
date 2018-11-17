# 119 Redis的哈希操作

* **添加**

```text
语法:
hset key field value

示例:
# 设置person键并定义person下的字段为field，字段对应的值为angle
hset person name angle
```

将哈希表key中的域field的值设为value

如果key不存在，一个新的哈希表被创建并进行HSET操作。如果域field已经存在于哈希表中，旧值将被覆盖

* **获取哈希中的field对应的值**

```text
语法:
hget key field

示例:
# 获取person下的字段的值
127.0.0.1:6379> hget person name
"angle"
```

* **删除key中的某个field**

```text
语法:
hdel key field[field...]

示例:
# 删除person下的name字段
hdel person name
```

```text
# 定义数据
127.0.0.1:6379> hset person name angle
(integer) 1
127.0.0.1:6379> hset person age 18
(integer) 1
127.0.0.1:6379> hset person sex boy
(integer) 1
```

* **获取某个哈希中所有的field和value**

```text
语法:
hgetall key

示例:
# 获取person下的所有的键值对
127.0.0.1:6379> hgetall person
1) "name"
2) "angle"
3) "age"
4) "18"
5) "sex"
6) "boy"
```

* **获取某个哈希中所有的字段**

```text
语法:
hkeys key

示例:
# 获取person下的所有的字段名
127.0.0.1:6379> hkeys person
1) "name"
2) "age"
3) "sex"
```

* **获取某个哈希中所有的值**

```text
语法:
hvals key

示例:
# 获取person下的所有字段的值
127.0.0.1:6379> hvals person
1) "angle"
2) "18"
3) "boy"
```

* **判断哈希中是否存在某个field**

```text
语法:
hexists key field

示例:
# 判断person中是否存在这个字段，存在返回1，否则返回0
127.0.0.1:6379> hexists person age
(integer) 1
127.0.0.1:6379> hexists person username
(integer) 0
```

* **获取哈希中总共的键值对**

```text
语法:
hlen key

示例:
# 判断person中有几个键值对
127.0.0.1:6379> hlen person
(integer) 3
```

