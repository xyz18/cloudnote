## 类

### 属性

1. 私有属性: 外部不能被访问
	
    在属性或方法的名称前面加上两个下划线, 即 `__`

2. 单个下划线

	`_`，表示不要随意访问这个变量，虽然它可以直接被访问

3. 双下划线

	以双下划线结尾（即 `__xxx__`）的变量是特殊变量

4. `__slots__`

* `__slots__` = ('x', 'y')
* 使用`__slots__` 来告诉 Python 只给一个固定集合的属性分配空间
* `__slots__` 设置的属性仅对当前类有效，对继承的子类不起效
除非子类也定义了`__slots__`，这样，子类允许定义的属性就是自身的 slots 加上父类的 slots。




### 对象

1. 对象类型

	type(obj)
	isinstance(obj, type)

2. 对象属性

* hasattr(obj, attr) 判断对象是否具有指定属性/方法；
* getattr(obj, attr[, default]) 获取属性/方法的值, 

	要是没有对应的属性则返回 default 值（前提是设置了 default），否则会抛出 AttributeError 异常；
    
* setattr(obj, attr, value) 设定该属性/方法的值，类似于 obj.attr=value；

3. 对象所有属性和方法名的列表
	
    dir(obj)

### 方法

1. 类方法

	@classmethod

2. 静态方法

	@staticmethod

3. 属性方法

	@property  只读方法属性
	@score.setter 	score方法属性可以赋值

4. 特殊方法	

|                 方法名                   |             描述          |
|-----------------------------------------|---------------------------|
| `__new__`                                   | 创建类实例, 先于__init__    |
| `__str__` , `__repr__`                      | print                     |
| `__iter__`, `__next__`                      | 迭代                      |
| `__getitem__`, `__setitem__`, `__delitem__` | obj[n] , del obj[n]      |
| `__getattr__`, `__setattr__`, `__delattr__` | 属性不存在的情况下才会被调用  |
| `__call__`                                  | obj()                     |
| `__enter__`, `__exit__`                     | 上下文管理器                |
| hasattr(obj, func)                          | 判断obj是否有方法func       |


### 调用父类

1. super().方法名(参数)     ||   	super(类名, self).方法名(参数)

```python
def super(cls, inst):
    mro = inst.__class__.mro()
    return mro[mro.index(cls) + 1]
```
	
* a. 获取 inst 的 MRO 列表
* b. 查找 cls 在当前 MRO 列表中的 index, 并返回它的下一个类，即 mro[index + 1]

> *cls 代表类，inst 代表实例*

> *super 其实和父类没有实质性的关联*

> *MRO 列表: 方法解析顺序( C.mro())*

### 元类

元类（metaclass）是用来创建类（对象）的可调用对象

1. type 就是一个元类。

```python
Foo = type('Foo', (object, ), {})    # 使用 type 创建了一个类对象
```

* 第 1 个参数是字符串 'Foo'，表示类名
* 第 2 个参数是元组 (object, )，表示所有的父类
* 第 3 个参数是字典，这里是一个空字典，表示没有定义属性和方法

2. 例子

* 类的方法和属性名称前面加上 `my_` 前缀
* 加一个 echo 方法

```python
class PrefixMetaclass(type):
	# cls：当前准备创建的类
	# name：类的名字
	# bases：类的父类集合
	# attrs：类的属性和方法，是一个字典
	def __new__(cls, name, bases, attrs):
		# 给所有属性和方法前面加上前缀 my_
		_attrs = (('my_' + name, value) for name, value in attrs.items())  

		_attrs = dict((name, value) for name, value in _attrs)  # 转化为字典
		_attrs['echo'] = lambda self, phrase: phrase  # 增加了一个 echo 方法

		return type.__new__(cls, name, bases, _attrs)  # 返回创建后的类


class Foo(metaclass=PrefixMetaclass):
	name = 'foo'
	def bar(self):
		print 'bar'
```

* Foo 中的`__init__`不执行
* 创建类: `__metaclass__`, 如果找不到, 用type创建

