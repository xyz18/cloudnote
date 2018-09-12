# Django

Django 是 Python 编程语言驱动的一个开源模型-视图-控制器（MVC）风格的 Web 应用程序框架.

MTV 模式：

| 层次 | 职责 |
|-|-|
| 模型(Model), 即数据存储层 | 处理与数据相关的所有事物，如何存取，如何验证有效性、包含哪些行为以及数据之间的关系等 |
| 模板(Template), 即表现层 | 处理与表现相关的决定，如何在页面或其他类型文档中进行显示 |
| 视图(View), 即业务逻辑层 | 存取模型及调取恰当模板的相关逻辑，模型与模板之间的桥梁|
## View : 衔接 HTTP 请求, 模板, 模型

* 业务逻辑函数: app/views.py
    * 模型处理数据
    * 渲染模板返回
        * HttpResponse: string
        * render: http
        * HttpResponseRedirect: 重定向
* 函数路由映射: app/urls.py
* 反向解析: 视图函数解析成url
    * 模板中: { % url '视图函数'%}
    * 代码: HttpResponseRedirect(reverse(视图函数))
* app路由映射: urls.py

## Model : 数据库调用

### 对象映射 : Python 类映射到数据库中的表

* app模型添加: settings.py (INSTALLED_APPS)
* 模型定义: app/models.py
    * 模型类的定义
    * 模型属性对应表的字段
    * 模型的 objects 对象实现模型数据的查询, 删除
    * 数据更新: 模型对象的 save 方法
    * 多表关系模型: `1:1, 1:N, M:N`
    * ORM
        * 抽象类继承
        * 多表继承
        * 代理模型继承
* 生成脚本: python manage.py makemigrations app
* 同步数据库: python manage.py migrate

### 表单 : 数据库表的一行数据记录, 也可以传入模板中作为参数

* 定义表单: app/forms.py
    * 表单绑定: form.is_bound
    * 表单验证
        * 字段属性验证: form.is_valid()
        * 自定义逻辑验证: ModelForm.clean()
* 修改模型: app/models.py (表单的一些默认值)
* 模板文件: app/templates/\*.html

### 模板管理 : 管理界面查看数据库表的内容

* 管理界面: app/admin.py
* 创建用户: python manage.py createsuperuser
* 登录地址: http://127.0.0.1:8000/admin/

## Template: 模板

* 变量替换: {{ ModelClass.var }}
* 过滤器: {{ ModelClass.var | upper }} 结果输出大写
* 流程控制
    * { % for i in line %} -- { % endfor %}
    * { % if id < 10 %} -- { % endif %}
* 模板继承
    * 父模板: { % block block_name %} -- { % endblock %}
    * 子模板
        * { % extends 父模板名称 %}: 指定父模板
        * { % block block_name %} -- { % endblock %}: 填充字段
        