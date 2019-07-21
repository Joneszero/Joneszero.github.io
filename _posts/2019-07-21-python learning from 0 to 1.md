---
layout:          post
title:           python learning from 0 to 1
subtitle:        python 变量
date:            2019-07-21
author:          Joneszero
header-img:        img/post1/post1_header_image.jpg
catalog:         true
tags:
    - python

---

> - python 学习我要开始记笔记了--

python语言中常见的几种变量类型有五种，分别是：

- **整型**：即整数，python3.x 中只有 int 一种。

- **浮点型**：即小数，除了数学写法（如`123.456`）之外还支持科学计数法（如`1.23456e2`）。

- **字符串型**：文本（单引号或者双引号），多行字符串可以用三个单引号或三个双引号开头，三个单引号或三个双引号结尾。

- **布尔型**：`True`、`False`两种值，要么是`True`，要么是`False`，请注意大小写，也可以通过布尔运算计算出来得到布尔值（例如`3 < 5`会产生布尔值`True`，而`2 == 1`会产生布尔值`False`）。

- **复数型**：形如`3+5j`，跟数学上的复数表示一样，唯一不同的是虚部的`i`换成了`j`。

  

python变量可以进行转变，可以使用python内置的函数：

- `int()`：将一个数值或字符串转换成整数，可以指定进制，二进制，十六进制等。
- `float()`：将一个字符串转换成浮点数。
- `str()`：将指定的对象转换成字符串形式，可以指定编码。



python占位符格式化：

| 占位符 |                                                    |
| ------ | -------------------------------------------------- |
| %s     | 字符串                                             |
| %d     | 整数                                               |
| %f     | 小数，可指定位数（%.2f 表示保留两位小数）          |
| %x     | 十六进制整数                                       |
| %%     | 转义，有时候%是一个普通字符，这时候用%%来表示一个% |

前面有几个占位符，后面就要跟着几个变量，一 一对应。



### 练习

#### 练习1：华氏温度转摄氏温度。

```python
f = float(input('请输入华氏温度: '))
c = (f - 32) / 1.8
print('%.1f华氏度 = %.1f摄氏度' % (f, c))
```

#### 

#### 练习2：输入圆的半径计算计算周长和面积。

```python
import math

radius = float(input('请输入圆的半径: '))
perimeter = 2 * math.pi * radius
area = math.pi * radius * radius
print('周长: %.2f' % perimeter)
print('面积: %.2f' % area)
```

#### 

#### 练习3：输入年份判断是不是闰年。

```python
year = int(input('请输入年份: '))
# 如果代码太长写成一行不便于阅读 可以使用\或()折行
is_leap = (year % 4 == 0 and year % 100 != 0 or
           year % 400 == 0)
print(is_leap)
```



参考资料：

[1] [廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/1016959663602400)

[2] [Python - 100天从新手到大师](https://github.com/jackfrued/Python-100-Days)