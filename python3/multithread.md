# 多线程

## 1. 函数, 创建线程

```python
t = threading.Thread(target=函数)     # 创建线程
t.start()                            # 开始线程
t.join()                             # 等待线程结束
```

## 2. 类继承threading.Thread, 创建线程

```python
class Thread_test(threading.Thread):
    
    def run(self):
        '''
            执行代码
        '''

t = Thread_test()
t.start()
t.join()
```

## 3. 线程池

```python
from multiprocessing.dummy import Pool as ThreadPool

p = ThreadPool(2)
p.map(函数, 参数列表)
p.close()
p.join()
```

## 线程属性
1) Python 解释器受到 GIL 锁的限制, python多线程只能使用1个核

    GIL 给所有线程都上了锁，多线程只能交替执行
    
2) `threading.current_thread().name`: 获取当前线程的名字

3) 线程锁

```python
lock = threading.Lock()     # 创建线程锁
...
look.acquire()              # 获取线程锁
修改语句
look.release()              # 释放线程锁
```

4) `multiprocessing.cpu_count()`  # CPU 个数

5) 减少局部变量传递

```python
local_school = threading.local()
...
local_school.student = 'one' # 赋值
# local_school.student是属于各自线程的

import threading
local_school = threading.local()    # 创建全局ThreadLocal对象:

def process_student():
    # 获取当前线程关联的student:
    std = local_school.student
    print('Hello, %s (in %s)' % (std, threading.current_thread().name))

def process_thread(name):
    # 绑定ThreadLocal的student:
    local_school.student = name
    process_student()

t1 = threading.Thread(target= process_thread, args=('Alice',), name='Thread-A')
t2 = threading.Thread(target= process_thread, args=('Bob',), name='Thread-B')
t1.start()
t2.start()
t1.join()
t2.join()
```