python函数的返回值，可以返回一个值，也能够返回多个值

### 单个值

```
def test():
    return 1

print(test())
```

运行结果

```
1
```

### 多个值

```
def test():
    return 'angle',18,[1,2,3]

print(test())
```

运行结果

```
('angle', 18, [1, 2, 3])
```

再返回多个值得时候，会打包成元组返回

