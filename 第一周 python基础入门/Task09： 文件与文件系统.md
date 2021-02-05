# Task09： 文件与文件系统

## 练习题

#### 1. 打开中文字符的文档时，会出现乱码，Python自带的打开文件是否可以指定文字编码？还是只能用相关函数？

可以，`open()`函数的`encoding`参数可以指定文字编码

#### 2. 编写程序查找最长的单词

输入文档: res/test.txt

```python
import string


def longest_word(filename):
    f = open(filename, encoding='utf-8')
    words = []
    for line in f.readlines():
        line = line.strip('\n')
        for i in string.punctuation:
            line = line.replace(i, '')
        words += line.split()
    words.sort(key=lambda x: len(x))
    longest = [i for i in words if len(i) == len(words[-1])]
    return longest
```

