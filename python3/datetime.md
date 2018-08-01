## time

|               time              |                    描述              |
|---------------------------------|--------------------------------------|
| time.daynight                   | 不等于0时，使用DST                     |
| time.altzone                    | 相对于UTC，DST偏移量，向东为负           |
| time.time()                     | 当前时间戳                             |
| time.timezone                   | 当前时区的偏移量（secs）                 |
| time.sleep(secs)                | 挂起线程secs秒                         |
| time.clock()                    | 第一次调用返回: time.clock语句所花费的时间 |
| time.clock()                    | 第二次调用返回自第一次调用到现在的运行时间   |
| time.gmtime([ts])               | 时间戳转UTC的struct_time                |
| time.localtime([ts])            | 时间戳转当地的struct_time               |
| time.mktime(st)                 | struct_time转当地时间戳                 |
| time.ctime([ts])                | 时间戳转字符串                          |
| time.asctime([st])              | struct_time转字符串                    |
| time.strftime(format[, st])     | struct_time 转字符串                   |
| time.strptime(string[, format]) | 字符串转struct_time                    |

| struct_time                     | 描述                                  |
|---------------------------------|--------------------------------------|
| st.tm_year                      | 年                                    |
| st.tm_mon                       | 月                                    |
| st.tm_mday                      | 日                                    |
| st.tm_hour                      | 时                                    |
| st.tm_min                       | 分                                    |
| st.tm_sec                       | 秒                                    |
| st.tm_wday                      | 一星期的第几天, 星期一(0)                |
| st.tm_yday                      | 一年中的第几天, [1, 366]                |
| st.tm_isdst                     | 判断是DST                              |
| st.tm_zone                      | 时区名                                 |
| st.tm_gmtoff                    | 距离UTC的偏移量(seconds)                |

### timedelta

|     timedelta      |            描述            |
|--------------------|----------------------------|
| td.total_seconds() | 总的时间(secs)             |
| td = dt1 - dt2     | datetime类型的时间运算结果 |

### datetime

| datetime | 描述 |
| -------- | --- |
| datetime.today()                                  | 当地的时间，无时区信息   |
| datetime.now(tz=None)                             | 当前时间                 |
| datetime.utcnow()                                 | 当前UTC时间，无时区      |
| datetime.fromtimestamp(ts, tz=None)               | 时间戳转时间             |
| datetime.utcfromtimestamp(ts)                     | 时间戳转UTC时间          |
| dt.timestamp()                                    | 时间转时间戳             |
| dt.timetuple()                                    | 时间转struct_time        |
| dt.utctimetuple()                                 | 时间转utc的struct_time   |
| datetime.strptime(string, format)                 | 字符串转时间             |
| dt.ctime()                                        | 时间转字符串             |
| dt.strftime(format)                               | 时间转字符串             |
| dt.year                                           | 年                       |
| dt.month                                          | 月                       |
| dt.day                                            | 日                       |
| dt.hour                                           | 时                       |
| dt.minute                                         | 分                       |
| dt.second                                         | 秒                       |
| dt.microsecond                                    | 微秒(百万分之一秒)       |
| dt.tzinfo                                         | 时区信息                 |
| dt.weekday()                                      | 星期一为0                |
| dt.isoweekday()                                   | 星期一为1                |
| dt.utcoffset()                                    | 时区的偏移量             |
| dt.tzname()                                       | 时区名                   |
| dt.astimezone(tz=None)                            | 时区转换(默认转当地时区) |
| dt.replace(...)                                   | 参数默认dt的值           |
| tz=datetime.timezone(datetime.timedelta(hours=7)) | 时区赋值                 |

#### format
| 指令 |描述|
|--|--|
| %y:  | 2个数字表示的年份 |
| %Y:  | 4个数字表示的年份|
| %m:  | 月份（[01,12]）|
| %b   | 月份的简写。如4月份为Apr|
| %B   | 月份的全写。如4月份为April|
| %d:  | 日在这个月中的天数（是这个月的第几天）|
| %j:  | 日在年中的天数 [001,366]（是当年的第几天）|
| %H:  | 小时（24小时制，[0, 23]）|
| %I:  | 小时（12小时制，[0, 11]）|
| %M:  | 分钟（[00,59]）|
| %S:  | 秒（范围为[00,61]，为什么不是[00, 59]，参考python手册~_~） |
| %f:  | 微秒（范围[0,999999]）|
| %z:  | 与utc时间的间隔 （如果是本地时间，返回空字符串）|
| %Z:  | 时区名称（如果是本地时间，返回空字符串）|
| %p:  | AM或者PM|
| %w:  | 今天在这周的天数，范围为[0, 6]，6表示星期天|
| %W:  | 周在当年的周数（是当年的第几周），星期一作为周的第一天|
| %U:  | 周在当年的周数当年的第几周），星期天作为周的第一天|
| %a   | 星期的简写。如 星期三为Web|
| %A   | 星期的全写。如 星期三为Wednesday|
| %x:  | 日期字符串（如：04/07/10）|
| %X:  | 时间字符串（如：10:43:39）|
| %c:  | 日期时间的字符串表示。（如： 04/07/10 10:43:39）|
| %%:  | %% => %|






