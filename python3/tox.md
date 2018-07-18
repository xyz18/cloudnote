## tox

tox是一个通用的虚拟环境管理和测试命令行工具. 所谓的虚拟环境，就是可以在一个主机上，自定义出多套的python环境，多套环境中使用不同的python拦截器，环境变量设置，第三方依赖包，执行不同的测试命令，最重要的是各个环境之间互不影响，相互隔离.

### 生成 tox.ini 文件

```bash
tox-quickstart
```

### tox 全局配置

```tox
[tox]  
envlist = py26,py27,pep8  
```

> *在命令行中直接执行 tox，就会依次执行 py26，py27，pep8*

### testenv 虚拟环境的配置

```tox
[testenv]
setenv =
    VIRTUAL_ENV={envdir}
    DISCOVER_DIRECTORY=sahara/tests/unit
deps =
    -r{toxinidir}/requirements.txt
    -r{toxinidir}/test-requirements.txt
commands = ostestr {posargs}
```
> *setenv列出了虚拟机环境中生效的环境变量，一些配色方案和单元测试标志；*

> *deps列出了虚拟环境需要的第三方依赖包*

> *commands就是在当前虚拟环境中需要执行的命令, 例: tox -- param1, 执行后就是 ostestr param1*

> *tox -e py27 -- param1: 指定Python环境执行 ostestr param1*

### pep8 代码静态检查

```tox
[testenv:pep8]
basepython = python3
deps =
  -c{env:UPPER_CONSTRAINTS_FILE:https://git.openstack.org/cgit/openstack/requirements/plain/upper-constraints.txt}
  -r{toxinidir}/requirements.txt
  -r{toxinidir}/test-requirements.txt
  -r{toxinidir}/doc/requirements.txt
commands =
    flake8 {posargs}
    doc8 doc/source
    # Run bashate checks
    bash -c "find sahara -iname '*.sh' -print0 | xargs -0 bashate -v"
    bash -c "find devstack -not -name \*.template -and -not -name README.rst -and -not -name \*.json -type f -print0 | xargs -0 bashate -v"
    # Run security linter
    bandit -c bandit.yaml -r sahara -n5 -p sahara_default -x tests
```

### 自定义命令行的虚拟机环境

```tox
[testenv:venv]
basepython = python3
commands = {posargs}
```

> *tox -e venv -- cmd1: 在虚拟环境中执行cmd1*

