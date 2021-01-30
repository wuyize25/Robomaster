# Task04：列表、元组和字符串

## 练习题

#### 1. 列表操作练习

列表`lst` 内容如下

`lst = [2, 5, 6, 7, 8, 9, 2, 9, 9]`

请写程序完成下列操作：

在列表的末尾增加元素`15`
在列表的中间位置插入元素`20`
将列表`[2, 5, 6]`合并到`lst`中
移除列表中索引为3的元素
翻转列表里的所有元素
对列表里的元素进行排序，从小到大一次，从大到小一次

```python
lst = [2, 5, 6, 7, 8, 9, 2, 9, 9]
lst.append(15)
lst.insert(int(len(lst) / 2), 20)
lst.extend([2, 5, 6])
lst.pop(3)
lst.reverse()
lst.sort()
lst.sort(reverse=True)
```

#### 2. 修改列表

问题描述：

`lst = [1, [4, 6], True]`

请将列表里所有数字修改成原来的两倍

```python
lst = [1, [4, 6], True]


def double_list(lst_):
    for i, value in enumerate(lst_):
        if isinstance(lst_[i], list):
            double_list(lst_[i])
        elif not isinstance(lst_[i], bool) and isinstance(lst_[i], int):
            lst_[i] *= 2


double_list(lst)
print(lst)
```

#### 3. LeetCode 852题 山脉数组的峰顶索引

如果一个数组k符合下面两个属性，则称之为山脉数组

数组的长度大于等于3

存在 $i$ ，$i>0$ 且 $i<\operatorname{len}(k)-1$， 使得
$$
\mathrm{k}[0]<\mathrm{k}[1]<\ldots<\mathrm{k}[\mathrm{i}-1]<\mathrm{k}[\mathrm{j}]>\mathrm{k}[\mathrm{i}+1] \ldots>\mathrm{k}[\operatorname{len}(\mathrm{k})-1]
$$
这个$i$就是顶峰索引。

现在，给定一个山脉数组，求顶峰索引。

示例:

输入：[1, 3, 4, 5, 3]

输出：True

输入：[1, 2, 4, 6, 4, 5]

输出：False

```python
lst = [1, 3, 4, 5, 3]
maxIndex = lst.index(max(lst))
isMountainArray = True
for i in range(0, len(lst)-1):
    if i < maxIndex:
        if lst[i] > lst[i+1]:
            isMountainArray = False
            break
    else:
        if lst[i] < lst[i+1]:
            isMountainArray = False
            break
print(isMountainArray)
if isMountainArray:
    print(maxIndex)
```

#### 4. 元组概念

写出下面代码的执行结果和最终结果的类型

```python
(1, 2)*2
# (1, 2, 1, 2) tuple
(1, )*2
# (1, 1) tuple
(1)*2
# 2 int
```

#### 5. 拆包过程是什么？

**拆包**：对于函数中的多个返回数据，去掉**元组**，**列表**或者**字典**直接获取里面数据的过程。

```
a, b = 1, 2
```

**上述过程属于拆包吗？**

不属于拆包，属于赋值。

**可迭代对象拆包时，怎么赋值给占位符？**

*代表取任意长，但是前后如果有定位的元素，优先给它们。

#### 6. 字符串函数回顾

- 怎么批量替换字符串中的元素？

  `replace(old, new [, max])` 将字符串中的`old`替换成`new`，如果`max`指定，则替换不超过`max`次。

- 怎么把字符串按照空格进⾏拆分？

  `split(str="", num)` 不带参数默认是以空格为分隔符切片字符串，如果`num`参数有设置，则仅分隔`num`个子字符串，返回切片后的子字符串拼接的列表。

- 怎么去除字符串⾸位的空格？

  `lstrip([chars])` 截掉字符串左边的空格或指定字符。

#### 7. 实现isdigit函数

题目要求

实现函数isdigit， 判断字符串里是否只包含数字0~9

```python
def isdigit(string):
    for i, j in enumerate(string):
        if not '0' <= j <= '9':
            return False
    return True
```

#### 8. LeetCode 5题 最长回文子串

给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

示例:

输入: `"babad"`

输出: `"bab"`

输入: `"cbbd"`

输出: `"bb"`

```python
class Solution:

    def longestPalindrome(self, s: str) -> str:
        temp, max_p, length = "", "", len(s)
        for index in range(length):
            index_left, index_right = index, index

            def compare(l, r):
                while l != -1 and r != length and s[l] == s[r]:
                    l, r = l - 1, r + 1
                return s[l + 1:r] if l == -1 or r == length else s[l + 1:r]

            temp = compare(index_left, index_right)
            max_p = temp if len(temp) > len(max_p) else max_p

            try:
                s[index + 1]
            except:
                continue

            if s[index] == s[index + 1]:
                left, right = index, index + 1
                temp = compare(left, right)
                max_p = temp if len(temp) > len(max_p) else max_p
        return max_p
```

