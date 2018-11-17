# 112 Python操作memcached

## 1.安装

```text
pip install python-memcached
```

## 2.建立连接

```text
mc = memcache.Client(["127.0.0.1:11211"],debug=True)
```

## 3.设置数据

```text
mc.set(key="name",val="angle",time=60,min_compress_len=5)

# 设置多个值
mc.set_multi({'title':r'小红帽','content':r'没有内容'},time=100)
```

## 4.获取数据

```text
mc.get('title')
```

## 5.删除数据

```text
mc.delete('name')
```

## 6.自增长

```text
# 默认自增加一,delta属性设置增加值
mc.incr('age',delta=10)
```

## 7.自减少

```text
mc.decr('age',delta=10)
```

```text
import memcache

# 连接
# 设置debug为true可以显示错误信息
# 在连接之前，要启动memcached服务
mc = memcache.Client(["127.0.0.1:11211"],debug=True)

# 设置
# time=0，永远不会过期
# key:键
# value:值
# mc.set(key="name",val="angle",time=60,min_compress_len=5)

# 设置多个值
# mc.set_multi({'title':r'小红帽','content':r'没有内容'},time=100)

# # 获取
# # print(mc.get("title"))
# username = mc.get('username')
# print(mc.get('username'))
#
# # 删除
# mc.delete('username')
# print(mc.get('username'))

# 默认自增加一,delta属性设置增加值
mc.incr('age',delta=10)
age = mc.get('age')
print(age)

# 自减少
mc.decr('age',delta=10)
age = mc.get('age')
print(age)
```

