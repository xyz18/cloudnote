## 贡献

### 提交 Bug 网站注册账号

注册 [Launchpad](https://launchpad.net/openstack) 账号, 加入 OpenStack 社区

### 提交代码网站注册账号

注册一个 [OpenStackID](https://www.openstack.org/profile), 成为 Foundation Member, 然后登录 [Gerrit Code Review](https://review.openstack.org), 在设置中配置如下信息:
* 填写 Profile 中的 Username
* 在 Agreements 签署协议
* 在 Contact Information 中填写 Foundation Member 的信息

### 配置本地环境

#### 安装git-view

```bash
$ sudo apt-get install git-review
```

#### 配置git

```bash
$ git config --global gitreview.username `Gerrit-Username`
$ git config --global user.name `Gerrit-Full Name`
$ git config --global user.email `Gerrit-Preferred Email`
$ git config --global gitreview.scheme https
$ git config --global gitreview.port 443
$ git config --global core.editor vim
```

### 克隆代码

```bash
$ git remote add gerrit https://`Gerrit-Username`:`Gerrit-HTTP PASSWORD`@review.openstack.org:443/openstack/sahara

$ cd sahara/.git/hooks
$ wget https://review.openstack.org/tools/hooks/commit-msg
$ chmod 755 commit-msg

$ git review -s -v
```

### 修改并提交代码

#### 创建分支

参照 Launchpad 上 Bug 的编号，根据 bug/${bug-number} 的命名规则创建并且切换 Branch。

```bash
$ git checkout -b bug/123456789
```

#### 在本地修复Bug

修改代码, 并提交到本地仓库 `git add`, `git commit`

提交信息的填写规范：

* 第一行：标题，概括你此次提交代码的功能或者目的。
* 第二行：换行。
* 第三行以及之后：具体地说明提交的内容、功能、目的等。
* 倒数第二行：换行。
* 最后一行：Closes-Bug:#xxx或者Partial-Bug: #xxx（其中xxx为bug的编号）。

可以通过 `git log` 查看提交信息

#### 新功能说明

```
pip install reno
tox -e venv -- reno new vanilla-2.7.5-support
```

#### 提交代码到社区

```bash
$ git review
```

在 [Gerrit Code Review](https://review.openstack.org) 上查看自己的修改

#### 社区交流

邮件：http://lists.openstack.org/pipermail/openstack-dev/
会议：http://eavesdrop.openstack.org/
贡献统计：http://stackalytics.com/
