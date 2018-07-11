## 文件系统

### 文件路径
| 方法 | 描述 |
|-|-|
| os.getcwd()   | 当前路径 |
| os.chdir(path) | 当前路径修改 |
| os.path.isabs(path) | 判断绝对路径 |
| os.path.abspath(path) | 相对路径转绝对路径 |
| os.path.exists(path) | 判断路径是否存在 |
| os.path.normpath(path) | 路径规范化 |
| os.path.join(path, * paths) | 路径合成 |
| os.listdir(path) | 列出路径下的所有文件 |
| glob.glob(path) | 路径搜索 |
| glob.glob(r"\*\*/\*.py", recursive=True)| 递归搜索路径 |

### 文件操作

| 方法 | 描述 |
|-|-|
| os.path.isfile(path) |	判断文件 |
| os.path.isdir(path) |	判断文件夹 |
| os.path.getctime(path) |	文件创建时间(windows) |
| os.path.getatime(path) |	文件访问时间 |
| os.path.getmtime(path) |	文件修改时间 |
| os.path.getsize(path) |	文件大小 |
| os.rename(ipath, opath) | 	文件重命名 |
| os.renames(idir, opath) | 	文件夹重命名 |
| shutil.move(ipath, opath) |  文件重命名 |
| shutil.copy(ipath, opath) | 	文件复制 |
| shutil.copytree(idir, odir) |	文件夹复制 |
| os.mkdir(path) |	创建一级文件夹 |
| os.makedirs(path) |	创建多级文件夹 |
| os.remove(path) 	| 删除文件 |
| os.rmdir(path) 	| 删除空文件夹 |
| os.removedirs(path) | 	删除多级空文件夹 |
| shutil.rmtree(path) | 	删除文件夹及其所有内容 |

