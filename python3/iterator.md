## 迭代工具

1. for循环
2. 列表解析
3. in成员关系测试
4. map内置函数
5. sorted
6. zip

## 可迭代对象

1. 实际序列
2. 按需求计算的虚拟序列	

## 迭代过程

1. 每次迭代调用obj.__next__()或next(obj), 迭代工具会自动调用next
	for line in open(file):
		print(line)
2. 捕捉StopIteration异常来确定何时离开


## 迭代器:

1. 文件迭代器
2. 字典迭代器

### 多迭代器

* range:      （多个迭代器）

> *i1 = iter(range对象) 产生第一个迭代器*

> *i2 = iter(range对象) 产生第二个迭代器*

### 单迭代器

* zip, map, 生成器:   （单个迭代器）

> *i1 = iter(zip对象) 产生第一个迭代器*

> *i2 = iter(zip对象) 引用第一个迭代器*


