## 环境安装

### Ubuntu

```bash
$ apt-get install gcc make zlib1g-dev libreadline-dev libssl-dev
```

### Centos

```bash
$ yum install gcc zlib-devel readline-devel openssl-devel sqlite-devel

$ tar -zxvf Python-3.*.*.tgz
$ cd Python-3.*.*
$ ./configure prefix=/opt/python-3.*.*
```

### Sublime Text

#### 安装 sublime text

* 官网下载 Windows 64 bit
* Add to explorer context menu
* 安装成功之后创建文件夹： Sublime Text 3/Data

#### 激活

> *3176版本*

```license
----- BEGIN LICENSE -----
sgbteam
Single User License
EA7E-1153259
8891CBB9 F1513E4F 1A3405C1 A865D53F
115F202E 7B91AB2D 0D2A40ED 352B269B
76E84F0B CD69BFC7 59F2DFEF E267328F
215652A3 E88F9D8F 4C38E3BA 5B2DAAE4
969624E7 DC9CD4D5 717FB40C 1B9738CF
20B3C4F1 E917B5B3 87C38D9C ACCE7DD8
5F7EF854 86B9743C FADC04AA FB0DA5C0
F913BE58 42FEA319 F954EFDD AE881E0B
------ END LICENSE ------
```

#### Package Control

* ctrl + shift + p
* Install Package Control

#### 主题设置

* Theme - SoDaReloaded
* Bubububububad and Boneyfied Color Schemes
    * 自定义 color schemes
    * http://tmtheme-editor.herokuapp.com/#!/editor/theme/Monokai
    * 另存为：Light.tmTheme
    * 添加 Light.tmTheme 到 Sublime Text 3\Data\Installed Packages\Bubububububad and Boneyfied Color Schemes.sublime-package

* 配置

```conf
{
    "color_scheme": "Packages/Bubububububad and Boneyfied Color Schemes/Light.tmTheme",
    "font_face": "Courier New",
    "font_size": 10,
    "ignored_packages":
    [
       "Vintage"
    ],
    "theme": "SoDaReloaded Light.sublime-theme",

    "translate_tabs_to_spaces": true,           //空格替代tab
    "highlight_line": true,                     //高亮显示当前行
    "show_encoding": true,                      //显示文件当前编码
    "bold_folder_labels": true,                 //加粗文件夹名称
    "word_wrap": true                           //自动换行
    // "trim_trailing_white_space_on_save": true,  //保存时去掉行尾无用空格
    // "save_on_focus_lost": true,                 //焦点丢失后自动保存
    
}
```

#### 快捷键

* Ctr + P:  快速切换打开文件，并且快速跳转文件中的symbols、line、word
    * [file]            匹配文件
    * [file]@[fun]      匹配函数 / 标题
    * [file]#[word]     匹配内容
    * [file]:lineNum    跳转到行


* Key Bindings

```conf
[
    { "keys": ["shift+enter"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Add Line.sublime-macro"} },
    { "keys": ["ctrl+h"], "command": "move", "args": {"by": "characters", "forward": false} },
    { "keys": ["ctrl+l"], "command": "move", "args": {"by": "characters", "forward": true} },
    { "keys": ["ctrl+k"], "command": "move", "args": {"by": "lines", "forward": false} },
    { "keys": ["ctrl+j"], "command": "move", "args": {"by": "lines", "forward": true} },
    { "keys": ["ctrl+1"], "command": "fold_by_level", "args": {"level": 1} },
    { "keys": ["ctrl+2"], "command": "fold_by_level", "args": {"level": 2} },
    { "keys": ["ctrl+3"], "command": "fold_by_level", "args": {"level": 3} },
    { "keys": ["ctrl+4"], "command": "fold_by_level", "args": {"level": 4} },
    { "keys": ["ctrl+5"], "command": "fold_by_level", "args": {"level": 5} },
    { "keys": ["ctrl+6"], "command": "fold_by_level", "args": {"level": 6} },
    { "keys": ["ctrl+7"], "command": "fold_by_level", "args": {"level": 7} },
    { "keys": ["ctrl+8"], "command": "fold_by_level", "args": {"level": 8} },
    { "keys": ["ctrl+9"], "command": "fold_by_level", "args": {"level": 9} },
    { "keys": ["ctrl+0"], "command": "unfold_all" },
]
```

#### Anaconda

{
    "enable_signatures_tooltip": false,
    "enable_docstrings_tooltip": false,
    "merge_signatures_and_doc": false,
    "pep8": false
}