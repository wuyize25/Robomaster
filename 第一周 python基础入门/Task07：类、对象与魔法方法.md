# Task07：类、对象与魔法方法

## 练习题

#### 1. 以下类定义中哪些是类属性，哪些是实例属性？

```python
class C:
    num = 0
    def __init__(self):
        self.x = 4
        self.y = 5
        C.count = 6
```

`num = 0`和`C.count = 6`是类属性

`self.x`和`self.y`是实例属性

#### 2. 怎么定义私有方法？

在 Python 中定义私有方法只需要在函数名前加上`__`两个下划线，那么这个函数就会为私有的了。

#### 3. 尝试执行以下代码，并解释错误原因：

```python
class C:
    def myFun():
        print('Hello!')
    c = C()
    c.myFun()
```

类的方法必须有一个额外的第一个参数名称（对应于该实例，即该对象本身），按照惯例它的名称是 `self`。

`c = C()`和`c.myFun()`应写到类外

#### 4. 按照以下要求定义一个游乐园门票的类，并尝试计算2个成人+1个小孩平日票价。

要求:

- 平日票价100元
- 周末票价为平日的120%
- 儿童票半价

```python
class Ticket:
    def __init__(self, isweekend = False, ischild = False):
        self.isWeekend = isweekend
        self.isChild = ischild

    def price(self):
        price = 120 if self.isWeekend else 100
        return price / 2 if self.isChild else price


adult = Ticket()
child = Ticket(False, True)
print(adult.price()*2 + child.price())
```

#### 5. 上面提到了许多魔法方法，如`__new__`, `__init__`, `__str__`, `__repr__`, `__getitem__`, `__setitem__`等等，请总结它们各自的使用方法。

- `__new__`方法是对象实例化时调用的第一个方法，该方法仅读取一个cls参数后再把其他参数都传给用于指明对象初始化行为的`__init__`方法，也就是说我们可以在一个对象初始化之前进行其他操作，比如检查是否合法等

- `__init__ ` 构造函数，在生成对象时调用
- `__str__`定义对类的实例调用`str()`时的行为
- `__repr__`是`__str__`的备胎.如果有`__str__`方法,那么先去执行`__str__`方法,并且使用`__str__`的返回值
- `__getitem__` 按照索引获取值
- `__setitem__`  按照索引赋值

#### 6. 利用python做一个简单的定时器类

要求:

- 定制一个计时器的类。

- `start`和`stop`方法代表启动计时和停止计时。

- 假设计时器对象`t1`，`print(t1)`和直接调用`t1`均显示结果。

- 当计时器未启动或已经停止计时时，调用`stop`方法会给予温馨的提示。

- 两个计时器对象可以进行相加：`t1+t2`。

- 只能使用提供的有限资源完成。

```python
import time


class Timer(object):
    def __init__(self):
        self.__info = '未开始计时！'
        self.__begin = None
        self.__end = None
        self.__jg = 0

    def __str__(self):
        return self.__info

    def __repr__(self):
        return self.__info

    def start(self):
        print('计时开始...')
        self.__begin = time.localtime()

    def stop(self):
        if not self.__begin:
            print('提示：请先调用start()开始计时！')
            return
        self.__end = time.localtime()
        self.__jg = time.mktime(self.__end) - time.mktime(self.__begin)
        self.__info = '运行了%d秒' % self.__jg
        print('计时结束！')
        return self.__jg

    def __add__(self, other):  
        return '共运行了%d秒' % (other.__jg + self.__jg)
```


