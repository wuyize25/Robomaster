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

