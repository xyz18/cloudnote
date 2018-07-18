## 制作安装包

Python 通过 setuptools 模块来打包和发布. setuptools 使用 pbr 模块进行参数配置. 即 pbr 将配置从 setup.py 隔离出来放在 setup.cfg 中，然后通过钩子在调用时将参数传递给 setup.py. pbr 能够根据 git 自动生成版本号、提取 Author 信息和 ChangeLog ，处理依赖及其他一些功能.

> *工程需要在 git 的跟踪下(git init)*

> *模块的版本号是从 `git tag` 下获取*

### setup.py

```python
import setuptools


setuptools.setup(
    setup_requires=["pbr>=2.0.0"],
    pbr=True
)
```

### setup.cfg

#### metadata

* name: 包的名称 (必须参数)


#### files

* packages: 安装工程下的模块

```
packages = 
    package1
    package2
```
> *packages如果省略, 默认metadata.name的值*

* data_files: 复制工程下的文件

```
data_files =
    fileDir =
        file1
        file2
```
> *fileDir 如果是相对路径, 根目录就是 sys.prefix, 否则 `site-packages/` 开始*
> *file1 是工程下的文件*
    
#### entry_points

对外暴露脚本接口, 可以在命令行直接执行 `cmd1`

```
group-name = 
    cmd1 = package1.file1.class1
    cmd2 = package2.file2.class2
```

##### 命令行执行

```bash
cmd1
```

##### pkg_resources 调用执行

```python
import pkg_resources


group = "group_name"
for entrypoint in pkg_resources.iter_entry_points(group=group):
    class1 = entrypoint.load()
```

```python
from pkg_resources import load_entry_point


group = "group_name"
dist = "package_name"
cmd1 = "cmd1"

class1 = load_entry_point(dist, group, cmd1)
```

