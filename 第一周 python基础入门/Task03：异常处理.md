# Task03：异常处理

## 练习题

#### 1. 猜数字游戏

电脑产生一个零到100之间的随机数字，然后让用户来猜，如果用户猜的数字比这个数字大，提示太大，否则提示太小，当用户正好猜中电脑会提示，"恭喜你猜到了这个数是......"。在用户每次猜测之前程序会输出用户是第几次猜测，如果用户输入的根本不是一个数字，程序会告诉用户"输入无效"。

```python
import random
num = random.randint(0, 100)
print("猜测一个0到100之间的整数")
time = 1
while True:
    try:
        guess = int(input("第"+str(time)+"次猜，请输入一个整形数字："))
        if guess == num:
            print("恭喜你猜到了这个数是" + str(num))
            break
        elif guess < num:
            print("太小")
        else:
            print("太大")
        time += 1
    except:
        print("输入无效")
```

