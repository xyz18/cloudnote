## 1. 生成器函数

编写为常规的def语句, 但是使用yield语句一次返回一个结果, 在每个结果之间挂起和继续它们的状态

例 1 : ( for )

```python
def ff(n):
	for i in range(n):
		yield i ** 2

for i in ff(5):
	print(i)
```

例 2 : ( send )

```python
def ff(n):
	for i in range(n):
		x = yield i ** 2
		print(x)

fid = ff(5)
print(next(fid))
print(fid.send(10))
```

## 2. 生成器表达式

```python
fid = ( x**2 for x in range(4) )
for i in fid:
	print(i)
```

## 应用到协程

```python
def consumer():
    r = ''
    while True:
        n = yield r
        if not n:
            return
        print('[CONSUMER] Consuming %s...' % n)
        r = '200 OK'

def produce(c):
    c.send(None)
    n = 0
    while n < 5:
        n = n + 1
        print('[PRODUCER] Producing %s...' % n)
        r = c.send(n)
        print('[PRODUCER] Consumer return: %s' % r)
    c.close()

c = consumer()
produce(c)
```
> *1. c.send(None) 等价于next(c) 运行生成器*

> *2. 使用 send() 方法给它发送消息；*

> *3. 使用 throw() 方法给它发送异常；*

> *4. 使用 close() 方法关闭生成器；*
	