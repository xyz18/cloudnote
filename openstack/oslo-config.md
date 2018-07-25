## oslo-config

oslo.config 模块是用来解析 OpenStack 中命令行（CLI）或配置文件（.conf）中的配置信息.

使用步骤:
* 定义选项信息(包括: 类型, 默认值, 说明)
* 注册选项到 config manager
* 执行解析(程序会从命令行和配置文件中提取注册的选项)

```python
from oslo_config import cfg
from oslo_config import types

PortType = types.Integer(1, 65535)
common_opts = [
    cfg.StrOpt('bind_host',
               default='0.0.0.0',
               help='IP address to listen on.'),
    cfg.Opt('bind_port',
            type=PortType,
            default=9292,
            help='Port number to listen on.')
]

file_opts = [
    cfg.StrOpt('name',
               default='admin',
               help='IP address to listen on.'),
    cfg.IntOpt('age',
               default=100,
               help='Port number to listen on.')
]

group_opts = [
    cfg.StrOpt('gname',
               default='gadmin',
               help='IP address to listen on.'),
    cfg.IntOpt('gage',
               default=111,
               help='Port number to listen on.')
]

CONF = cfg.CONF
CONF.register_cli_opts(common_opts)
CONF.register_opts(file_opts)

rabbit_group = cfg.OptGroup(name='rabbit',
                            title='RabbitMQ options')
CONF.register_group(rabbit_group)
CONF.register_opts(group_opts, group=rabbit_group)
# CONF.register_opts(group_opts, group="rabbit")

CONF()

print(CONF.age)
print(CONF.rabbit.gname)
```

### 定义选项信息

* cfg.StrOpt 是内部定义好的类型
* cfg.Opt 可以指定自定义类型(PortType)

### 将选项注册到 config manager

注册选项有两种方式: 

* 命令行选项注册(register_cli_opts)
* 文件选项注册(register_opts)

这两种方式注册的唯一区别是显示命令行注册可以在命令行 `--help` 查看有哪些选项可以设置. 除此之外, 没有区别, 命令行中的参数可以设置文件注册的选项, 文件中的参数也可以设置命令行注册的选项.

文件选项注册默认组是 DEFAULT, 也可以指明组 `CONF.register_opts(group_opts, group="rabbit")`

### 执行解析

CONF() 解析命令行（CLI）或配置文件（.conf）中的配置信息.

* 默认搜索 ~/.${project}， ~/， /etc/${project} 的 {prog}.conf 文件

#### default_config_dirs

可以指定搜索配置文件的路径

#### default_config_files

可以指定搜索配置文件, 会屏蔽掉配置文件的搜索

#### project

默认None, 设置 project 作用于搜索路径

#### prog

默认主程序名称, 设置 prog 作用于搜索的配置文件名
