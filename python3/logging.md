### logging 设计模块

1. Loggers 把应用需要直接调用的接口暴露出来.
2. Handlers 把 log 记录发到相应的目的地.
3. Filters 决定哪些记录需要发给 handler.
4. Formatters 定义了 log 记录的输出格式


#### Logger

1. logging.root 是模块内定义的 Logger
2. 自定义 Logger
    uu = logging.getLogger(name)
3. logging.info 默认 logging.root 对象的方法
    自定义：uu.info
4. 设置日志级别
    root.setLevel(logging.WARNING)


#### Handler

1. 输出到文件
    handler = logging.FileHandler(filename)

2. 输出到控制台
    handler = logging.StreamHandler()

3. 间隔一段时间自动创建日志
    handler = logging.handlers.TimedRotatingFileHandler(filename, when='M', interval=1, backupCount=7, encoding='utf-8', utc=False)

    1) M:           1分钟后重新创建日志
    2) interval:    间隔几个when
    3) backupCount: 日志存储数量
    4) 没有日志输出时，不会创建文件

#### Formatter

创建日志格式对象

### 执行用例

```python
logger = logging.getLogger(name)
handler = logging.StreamHandler()
fmt = logging.Formatter('[%(asctime)s] %(module)-10.10s %(lineno)4d.%(levelname)s: %(message)s')

handler.setFormatter(fmt)
logger.addHandler(handler)
```

### 封装成工具用例

```python
import logging
import logging.handlers
import os
 
log_file = None
 
def beg_info(os_file=None):
    global log_file
    if os_file:
        log_file = os_file
 
    set(level=logging.INFO, os_file=log_file, fmt='%(message)s')
    logging.info('')
 
    set(level=logging.INFO, os_file=log_file, fmt='            Begin: %(asctime)s ')
    logging.info('')
    set(level=logging.INFO, os_file=log_file, fmt='%(message)s')
 
    logging.info('')
    logging.info('*************************')
    set(level=logging.INFO, os_file=log_file)
    

def end_info(os_file=None):
    global log_file
    if os_file:
        log_file = os_file
 
    set(level=logging.INFO, os_file=log_file, fmt='%(message)s')
    logging.info('*************************')
    logging.info('')
 
    set(level=logging.INFO, os_file=log_file, fmt='            End: %(asctime)s ')
    logging.info('')
    set(level=logging.INFO, os_file=log_file, fmt='%(message)s')
 
    logging.info('')
    logging.info('***************************************************************************')


def set(level=logging.WARNING, os_file=None, fmt=None):
    global log_file
    if os_file:
        log_file = os_file
    # '''
    #     Logger
    # '''
    root = logging.root             #   相当于: ll = logging.getLogger(name)
    root.setLevel(level)     # 指定日志级别，低于lel级别的日志将被忽略
 
 
    # '''
    #                 fileHandler:                输出到文件
    #     Handler     StreamHandler:              输出到控制台
    #                 TimedRotatingFileHandler:   间隔一段时间自动创建新日志
    # '''
    if not log_file:
        curdir = os.path.abspath(os.curdir)
        log_file = os.path.join(curdir, 'log.log')
    # fileHandler = logging.FileHandler(log_file)
    consoleHandler = logging.StreamHandler()
    timeHandler = logging.handlers.TimedRotatingFileHandler(log_file, when='midnight', 
        interval=1, backupCount=7, encoding='utf-8', utc=False)
 
    handle = timeHandler
 

    # '''
    #     Formatter
    # '''
    if fmt==None:
        fmt = logging.Formatter('[%(asctime)s] %(module)15.15s %(lineno)4d.%(levelname)s: %(message)s')
    else:
        fmt = logging.Formatter(fmt)
 
     
 
    handle.setFormatter(fmt)
    root.handlers = []
    root.addHandler(handle)
    consoleHandler.setFormatter(fmt)
    root.addHandler(consoleHandler)
 
    # timeHandler.setFormatter(fmt)
    # root.addHandler(timeHandler)
 
    return
```    
