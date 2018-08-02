# 多进程

## 1. fork() : (Unix / Linux)

* 1) 复制一份当前进程（主进程，整个地址空间的拷贝），生成子进程
* 2) 分别在父进程和子进程内返回
* 3) 父进程fork()返回子进程的ID
* 4) 子进程fork()返回0

    
### a. 进程获取

os.getpid()     # 获取自身ID

os.getppid()    # 获取父进程ID
    
### b. 进程区分

选择语句：

```python
if pid: # 父进程
    pass
else:   # 子进程
    pass
```

### c. 进程通信

os.pipe() # 创建管道

    一个管道包括两个端，一个读(父进程), 一个写(子进程)

所以，运行过程是：

```
       ---创建管道
       ---创建子进程。

子进程：

       ----需要关闭管道读端
       ----开始执行
       ----向写端写入结果
       ----进程死亡

父进程：

       ----关闭管道写端
       ----从读端读取数据直到子进程死亡或者关闭
       ----调用waitpid方法确保子进程已经被撤销（在FreeBSD中不这么做，那么子进程永远不会被死亡）
       ----进程输出
```

### d. 代码

```python
import os, sys

r, w = os.pipe()
pid = os.fork()

if pid: # parent
    os.close(w)
    r = os.fdopen(r)
    print("parent:reading")
    txt = r.read()
    os.waitpid(pid, 0)
else:   # child
    os.close(r)
    w = os.fdopen(w, 'w')
    print('child: writing')
    w.writing("here's some text from the child")
    w.close()
    print('child: closing')
    sys.exit(0)

print("parent: got it: text= ", txt)
```

## 2. multiprocessing

* 1) 模块导入的时候不被允许执行进程, 进程不能在模块顶层执行
* 2) 进程间的通信使用multiprocessing.Queue或os.pipe, 传入进程的参数
* 3) p.terminate() # 强制进程停止

### a. Process

```python
p = Process(target=函数, args=元组参数)    # 创建进程
p.start()                                  # 启动进程
p.join()                                   # 等待进程结束
```

### b. Pool：进程池

```python
p = Pool(4)                                  # 创建进程，最多同时进行4个
for i in range(n): # 共有n多个任务
    p.apply_async(函数, args=元组参数)
p.close()                                    # 不能在添加新进程
p.join()                                     # 等待进程结束
```

### c. subprocess: 外部进程

* 直接执行

    `subprocess.call(['nslookup', 'www.python.org'])`

    相当于在命令行运行: `nsloopup www.python.org`


* 返回结果

```python
p = subprocess.Popen(['nslookup'],   # 输入命令
    stdin=subprocess.PIPE, 
    stderr=subprocess.PIPE,
    stdout=subprocess.PIPE)

output, err = p.communicate(b'set q=mx\npython.org\nexit\n') # 输入参数

print(output.decode('gbk')) # 输出结果
```



