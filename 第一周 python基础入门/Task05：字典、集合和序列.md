# Task05：字典、集合和序列

## 练习题

#### 1. 字典基本操作

字典内容如下:

```
dic = {
    'python': 95,
    'java': 99,
    'c': 100
    }
```

用程序解答下面的题目

- 字典的长度是多少

  ```python
  print(len(dic))
  ```

- 请修改`'java'`这个key对应的value值为`98`

  ```python
  dic['java'] = 98
  ```

- 删除 c 这个key

  ```python
  del dic['c']
  ```

- 增加一个key-value对，key值为 `php`, value是`90`

  ```python
  dic['php'] = 90
  ```

- 获取所有的key值，存储在列表里

  ```python
  keys = list(dic.keys())
  ```

- 获取所有的value值，存储在列表里

  ```python
  values = list(dic.values())
  ```

- 判断 `javascript` 是否在字典中

  ```python
  isJavascriptInDict = 'javascript' in dic
  ```

- 获得字典里所有value 的和

  ```python
  Sum = sum(values)
  ```

- 获取字典里最大的value

  ```python
  Max = max(values)
  ```

- 获取字典里最小的value

  ```python
  Min = min(values)
  ```

- 字典 `dic1 = {'php': 97}`， 将`dic1`的数据更新到`dic`中

  ```python
  dic.update(dic1)
  ```

#### 2. 字典中的value

有一个字典，保存的是学生各个编程语言的成绩，内容如下

```python
data = {
        'python': {'上学期': '90', '下学期': '95'},
        'c++': ['95', '96', '97'],
        'java': [{'月考': '90', '期中考试': '94', '期末考试': '98'}]
        }
```

各门课程的考试成绩存储方式并不相同，有的用字典，有的用列表，但是分数都是字符串类型，请实现函数`transfer_score(score_dict)`，将分数修改成int类型

```python
def transfer_score(data):
    if isinstance(data, dict):
        items = data.items()
    elif isinstance(data, list):
        items = enumerate(data)
    if items:
        for key, value in items:
            try:
                data[key] = int(data[key])
            except:
                data[key] = transfer_score(data[key])
    return data
```

#### 3. 怎么表示只包含⼀个数字1的元组

```python
tup = (1,)
```

#### 4. 创建一个空集合，增加 `{'x', 'y', 'z'}` 三个元素

```python
s = set()
s.update({'x', 'y', 'z'})
```

#### 5. 列表`['A', 'B', 'A', 'B']`去重

```python
s = set(['A', 'B', 'A', 'B'])
```

#### 6. 求两个集合{6, 7, 8}，{7, 8, 9}中不重复的元素（差集指的是两个集合交集外的部分）

```python
s = {6, 7, 8} ^ {7, 8, 9}
```

#### 7. 求{'A', 'B', 'C'}中元素在 {'B', 'C', 'D'}中出现的次数

```python
count = len({'A', 'B', 'C'} & {'B', 'C', 'D'})
```

#### 8. 怎么找出序列中的最大、小值？

- `max(sub)`返回序列或者参数集合中的最大值
- `min(sub)`返回序列或参数集合中的最小值

#### 9. sort() 和 sorted() 区别

- sort 是应用在 list 上的方法，属于列表的成员方法，sorted 可以对所有可迭代的对象进行排序操作。
- list 的 sort 方法返回的是对已经存在的列表进行操作，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。
- sort使用方法为`ls.sort()`，而sorted使用方法为`sorted(ls)`

#### 10. 怎么快速求 1 到 100 所有整数相加之和？

```python
sum(range(1, 101))
```

#### 11. 求列表 [2,3,4,5] 中每个元素的立方根

```python
l = [2, 3, 4, 5]
for i, j in enumerate(l):
    l[i] = l[i] ** (1/3)
```

#### 12. 将[‘x’,‘y’,‘z’] 和 [1,2,3] 转成 [(‘x’,1),(‘y’,2),(‘z’,3)] 的形式

```python
zipped = list(zip(['x', 'y', 'z'], [1, 2, 3]))
```

