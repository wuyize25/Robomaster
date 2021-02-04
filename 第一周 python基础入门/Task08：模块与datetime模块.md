# Task08：模块与datetime模块

## 练习题

#### 1. 怎么查出通过 from xx import xx导入的可以直接调用的方法？

`help(xx.xx)`

#### 2. 了解Collection模块，编写程序以查询给定列表中最常见的元素。

题目说明：

输入：language = ['PHP', 'PHP', 'Python', 'PHP', 'Python', 'JS', 'Python', 'Python','PHP', 'Python']

输出：Python

```python
"""
Input file
language = ['PHP', 'PHP', 'Python', 'PHP', 'Python', 'JS', 'Python', 'Python','PHP', 'Python']

Output file
Python
"""
from collections import Counter


def most_element(language):
    """ Return a list of lines after inserting a word in a specific line. """
    count = Counter(language)
    result = count.most_common(1)
    return result[0][0]
```

#### 3. 假设你获取了用户输入的日期和时间如`2020-1-21 9:01:30`，以及一个时区信息如`UTC+5:00`，均是`str`，请编写一个函数将其转换为timestamp：

```python
from datetime import datetime


def to_timestamp(dt_str, tz_str):
    tz = tz_str.split(':')
    if len(tz[0]) == 5:
        tz[0] = tz[0][0:4]+'0'+tz[0][4]
    dt = datetime.strptime(dt_str+tz[0]+tz[1], "%Y-%m-%d %H:%M:%SUTC%z")
    return dt.timestamp()
```

#### 4. 编写Python程序以选择指定年份的所有星期日

```python
def all_sundays(year):
    year = int(year)
    dt1 = datetime.date(year, 1, 1)
    dt2 = datetime.date(year+1, 1, 1)
    for i in range((dt2 - dt1).days):
        day = dt1 + datetime.timedelta(days=i)
        if day.isoweekday() == 7:
            print(day)
```
