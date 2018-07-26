## 内置类型

python 中主要的内置类型有：
* numerics
* sequences
* mappings
* classes
* instances
* exceptions

### 布尔型

| Boolean | 描述 |
|---------|------|
| True    |  真  |
| False   |  假  |

### 整型和浮点型

|  int / float  |      描述     |
|---------------|---------------|
| x / y         | 浮点除        |
| x // y        | 整数除        |
| abs(x)        | 绝对值        |
| round(x)      | 四舍五入      |
| math.trunc(x) | 截断          |
| math.floor(x) | 地板          |
| math.ceil(x)  | 天花板        |
| x &#124; y    | 按位或（int） |
| x ^ y         | 按位异或      |
| x & y         | 按位与        |
| x << n        | 按位左移      |
| x >> n        | 按位又移      |
| ~x            | 按位取反      |



|                  int / float                   |          描述         |
|------------------------------------------------|-----------------------|
| x.bit_length()                                 | 内存中有效bites的长度 |
| x.to_bytes(length, byteorder, signed=False)    | int 转 bytes          |
| int.from_bytes(bytes, byteorder, signed=False) | signed=True则x为负数  |
| y.is_integer()                                 | 判断小数为0           |


### 列表

|       list      |             描述             |
|-----------------|------------------------------|
| ll.index(val)   | 列表中等于val的索引          |
| ll.reverse()    | 反转                         |
| len(ll)         | 长度                         |
| ll.count(x)     | 等于x的元素数量              |
| ll.append(x)    | 追加一个元素                 |
| ll.extend(ll_2) | 追加ll_2中的所有元素         |
| ll *= n         | 复制n次                      |
| ll.insert(i, x) | i处插入x                     |
| ll[i:j] = list  | 插入列表                     |
| del ll[i:j]     | 删除                         |
| ll.remove(val)  | 删除等于val的元素(仅一个)    |
| ll.clear()      | 清空                         |
| ll.pop(i)       | del ll[i], 默认ll[len(ll)-1] |



### 字符串

|                str                 |           描述          |
|------------------------------------|-------------------------|
| ss.isalnum()                       | 判断都是字母或数字      |
| ss.isalpha()                       | 判断都是字母            |
| ss.isdigit()                       | 判断都是数字            |
| ss.islower()                       | 判断都是小写            |
| ss.isupper()                       | 判断都是大写            |
| ss.isspace()                       | 判断都是空格            |
| ss.encode()                        | str转bytes              |
| bb.decode()                        | bytes转str              |
| ss.join(strlist)                   | 用ss连接strlist         |
| ss.capitalize()                    | 首字母大写，其他小写    |
| ss.lower()                         | 字母小写                |
| ss.upper()                         | 字母大写                |
| ss.swapcase()                      | 大小写互换              |
| ss.zfill(width)                    | 数字字符串左添加0 [+-]  |
| ss.center(width[, fillchar])       | 两边填充                |
| ss.ljust(width[, fillchar])        | 左填充                  |
| ss.rjust(width[, fillchar])        | 右填充                  |
| ss.endswith(sub[, start[, end]])   | 判断字符串以sub结束     |
| ss.startwith(sub[, start[, end]])  | 判断字符串以sub开始     |
| ss.strip([chars])                  | 两边删除                |
| ss.lstrip([chars])                 | 左删除                  |
| ss.rstrip([chars])                 | 右删除                  |
| ss.split(sep=None, maxsplit=-1)    | 分割                    |
| ss.cout(sub[, start[, end]])       | sub的数量               |
| ss.find(sub[, start[, end]])       | 查询sub的第一个位置索引 |
| ss.replace(old, new[, count])      | 替换(默认替换所有)      |
| ss.translate(table[, deletechars]) | 单字符映射替换          |


### 正则表达式

|    符号    |  描 述                                   |     正则表达式示例   |
|------------|-----------------------------------------|-------------------|
| literal    | 匹配文本字符串的字面值literal               | foo               |
| re1 &#124; re2 | 匹配正则表达式re1 或者re2              | foo &#124; bar     |
| .          | 匹配任何字符（除了\n 之外）                 | b.b                |
| ^          | 匹配字符串起始部分                         | ^Dear              |
| $          | 匹配字符串终止部分                         | /bin/*sh$          |
| *          | 匹配0 次或者多次前面出现的正则表达式          | [A-Za-z0-9]*       |
| +          | 匹配1 次或者多次前面出现的正则表达式          | [a-z]+\.com        |
| ?          | 匹配0 次或者1 次前面出现的正则表达式          | goo?               |
| {N}        | 匹配N 次前面出现的正则表达式                 | [0-9]{3}           |
| {M,N}      | 匹配M～N 次前面出现的正则表达式              | [0-9]{5,9}         |
| […]        | 匹配来自字符集的任意单一字符                 | [aeiou]            |
| [..x−y..]  | 匹配x～y 范围中的任意单一字符                | [0-9], [A-Za-z]    |
| [^…]       | 不匹配此字符集中出现的任何一个字符，包括某一范围的字符（如果在此字符集中出现） | [^aeiou], [^A-Za-z0-9] |
| (*&#124;+&#124;?&#124;{})?| 用于匹配上面频繁出现/重复出现符号的非贪婪版本 |（*、+、?、{}） .*?[a-z]|
| (…)        | 匹配封闭的正则表达式，然后另存为子组          | ([0-9]{3})?,f(oo&#124;u)bar |


| 特殊字符 |    描述      | 正则表达式示例 |
|----------|-----|----------------|
| \d       | 匹配任何十进制数字，与[0-9]一致（\D 与\d 相反，不匹配任何非数值型的数字） | data\d+.txt  |
| \w       | 匹配任何字母数字字符，与[A-Za-z0-9_]相同（\W与之相反）  | [A-Za-z_]\w+   |
| \s       | 匹配任何空格字符，与[\n\t\r\v\f]相同（\S 与之相反）     | of\sthe        |
| \b       | 匹配任何单词边界（\B 与之相反）                        | \bThe\b       |
| \N       | 匹配已保存的子组N（参见上面的(…))                       | price: \16   |
| \c       | 逐字匹配任何特殊字符c（即，仅按照字面意义匹配，不匹配特殊含义）| \., \\, \*  |
| \A(\Z)   | 匹配字符串的起始（结束）（另见上面介绍的^和$）              | \ADear      |

|    扩展表示法    |                                   描述                                  |  正则表达式示例   |
|------------------|-------------------------------------------------------------------------|-------------------|
|    (?iLmsux)     |    在正则表达式中嵌入一个或者多个特殊“标记”参数（或者通过函数/方法）    | （?x），（？ im） |
|      (?:…)       |                       表示一个匹配不用保存的分组                        |     (?:\w+\.)*    |
|   (?P<name>…)    |           像一个仅由name 标识而不是数字ID 标识的正则分组匹配            |     (?P<data>)    |
|    (?P=name)     |               在同一字符串中匹配由(?P<name)分组的之前文本               |     (?P=data)     |
|      (?#…)       |                       表示注释，所有内容都被忽略                        |    (?#comment)    |
|      (?=…)       |  匹配条件是如果…出现在之后的位置，而不使用输入字符串；称作正向前视断言  |      (?=.com)     |
|      (?!…)       | 匹配条件是如果…不出现在之后的位置，而不使用输入字符串；称作负向前视断言 |      (?!.net)     |
|      (?<=…)      |  匹配条件是如果…出现在之前的位置，而不使用输入字符串；称作正向后视断言  |     (?<=800-)     |
|      (?<!…)      | 匹配条件是如果…不出现在之前的位置，而不使用输入字符串；称作负向后视断言 |  (?<!192\.168\.)  |
| (?(id/name)Y&#124;N ) |   如果分组的id 或者name存在，就返回条件匹配Y，否则返回N；|N 是可选项    |     (?(1)y&#124;x)     |


|                  re                  |      描述     |
|--------------------------------------|---------------|
| compile(pattern, flags = 0)          | 使用任何可选的标记来编译正则表达式的模式，然后返回一个正则表达式对象   |
| match(pattern, string, flags=0)      | 尝试使用带有可选的标记的正则表达式的模式来匹配字符串。返回匹配对象     |
| search(pattern，string，flags=0)     | 使用可选标记搜索字符串中第一次出现的正则表达式模式。返回匹配对象       |
| findall(pattern，string [, flags] )  | 查找字符串中所有（非重复）出现的正则表达式模式，并返回一个匹配列表     |
| finditer(pattern，string [, flags] ) | 与findall()函数相同，但返回的不是一个列表，而是一个迭代器。         |
| split(pattern，string，max=0)        | 根据正则表达式的模式分隔符, 将字符串分割为列表, 返回成功匹配的列表     |
| sub(pattern，repl，string，count=0)  | 使用repl 替换所有正则表达式的模式在字符串中出现的位置，替换所有位置(0) |
| purge()                              | 清除隐式编译的正则表达式模式                                    |
| group(num=0)                         | 返回整个匹配对象，或者编号为num 的特定子组                        |
| groups(default=None)                 | 返回一个包含所有匹配子组的元组（如果没有成功匹配，则返回一个空元组）   |
| groupdict(default=None)              | 返回一个包含所有匹配的命名子组的字典，所有的子组名称作为字典的键      |
| re.I、re.IGNORECASE                  | 不区分大小写的匹配                                             |
| re.L、re.LOCALE                      | 根据所使用的本地语言环境通过\w、\W、\b、\B、\s、\S 实现匹配       |
| re.M、re.MULTILINE                   | ^和$分别匹配目标字符串中的起始和结尾，而不是严格匹配整个字符串的起始和结尾 |
| re.S、rer.DOTALL                     | 该标记表示“.”（点号）能够匹配全部字符                            |
| re.X、re.VERBOSE                     | 通过反斜线转义, 否则所有空格加上#都被忽略, 除非允许注释           |


### 集合

|        set        |       描述       |
|-------------------|------------------|
|                   |                  |
| x.add(elem)       | 添加             |
| x.union(y)        | 更新             |
| x.remove(elem)    | 删除             |
| x.discard(elem)   | 删除             |
| x.clear()         | 清除             |
| x.intersection(y) | 交集             |
| x.union(y)        | 并集             |
| x.issubset(y)     | 判断x是y的子集   |
| x.disjoint(y)     | 判断x和y没有交集 |
| x &#124; y        | 并集             |
| x & y             | 交集             |
| x ^ y             | 异或             |
| x - y             | 差集             |

### 字典

|              dict             |          描述          |
|-------------------------------|------------------------|
| len(dd)                       | 元素个数               |
| key in dd                     | 判断key是否属于dd      |
| dd.get(key[, default])        | 取key对应的value值     |
| dd.update([other])            | 更新                   |
| del dd[key]                   | 删除                   |
| dd.clear()                    | 清除                   |
| d1.popitem()                  | 随机移除               |
| dd.setdefault(key[, default]) | 设置key对应的值        |
| dd.values()                   | value对应的列表        |
| dd.keys()                     | key对应的列表          |
| dd.items()                    | (key, value)对应的列表 |
| dd.copy()                     | 浅复制                 |


> 深复制

```python
from copy import deepcopy

dd = deepcopy(d1)
```



