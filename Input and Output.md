# 格式化输出

- 使用格式化字符串
在字符串之前加上`f`或`F`，在字符串中花括号`{}`内写入Python表达式，表达式的值将被带入，即可打印表达式的内容

```python
year = 2016
event = 'Referendum'
f'Results of the {year} {event}'
# 'Results of the 2016 Referendum'
```

- 使用字符串`str.format()`的方法

仍然可以使用`{}`标记将替换变量的位置，并提供详细的格式化指令。

```python
yes_votes = 42_572_654
no_votes = 43_132_495
percentage = yes_votes / (yes_votes + no_votes)
'{:-9} YES votes {:2.2%}'.format(yes_votes, percentage)
# ' 42572654 YES votes  49.67%'
```

如果不需要花式输出，只想尽快显示某些变量以便进行调试，可以使用`repr()`或者`str()`函数将任何值转换为字符串。

```python
>>> s = 'Hello, world.'
>>> str(s)
'Hello, world.'
>>> repr(s)
"'Hello, world.'"
>>> str(1/7)
'0.14285714285714285'
>>> x = 10 * 3.25
>>> y = 200 * 200
>>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
>>> print(s)
The value of x is 32.5, and y is 40000...
>>> # The repr() of a string adds string quotes and backslashes:
... hello = 'hello, world\n'
>>> hellos = repr(hello)
>>> print(hellos)
'hello, world\n'
>>> # The argument to repr() may be any Python object:
... repr((x, y, ('spam', 'eggs')))
"(32.5, 40000, ('spam', 'eggs'))"
```

## 7.1.1 格式字符串(f-string)

通过在字符串前面加上`f`或`F`的前缀并将表达式写为`{expression}`，可以将Python表达式的值包含在字符串中。

```python
>>> import math
>>> print(f'The value of pi is approximately {math.pi:.3f}.')
The value of pi is approximately 3.142.
```

在`:`之后传递一个整数将导致该字段为最小字符宽度。

```python
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
for name, phone in table.items():
    print(f'{name:10} ==> {phone:10d}')
# Sjoerd     ==>       4127
# Jack       ==>       4098
# Dcab       ==>       7678
```

其它修饰符可用于在格式化值之前对其进行转换。

- `!a`表示`ascii()`
- `!s`表示`str()`
- `!r`表示`repr()`

```python
>>> animals = 'eels'
>>> print(f'My hovercraft is full of {animals}.')
My hovercraft is full of eels.
>>> print(f'My hovercraft is full of {animals!r}.')
My hovercraft is full of 'eels'.
```

## 7.1.2 The String format() Method

```python
>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
# We are the knights who say "Ni!"
```

其中的花括号和字符(称为格式字段)被替换为`str.format()`传入的对象。花括号中的数字可以指定传入对象的位置。

```python
>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam
```

如果在`str.format()`方法中使用关键字参数，则通过使用参数的名字来引用它们的值。

```python
print('This {food} is {adjective}.'.format(
        food='spam', adjective='absolutely horrible'))
# This spam is absolutely horrible.

print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
                                                 other='hello'))
# The story of Bill, Manfred, and hello.
```

例子：

```python
# 小数
"{:.3f}.format(3.1415926)"  # 3.142
"{:.0f}.format(3.1415926)"  # 3
"{:+.3f}.format(3.1415926)"  # +3.142
"{:-.3f}.format(-3.1415926)"  # -3.142
# 格式化对齐
"{:g^10}".format(10)    # gggg10gggg
"{:g>10}".format(10)    # gggggggg10
"{:g<10}".format(10)    # 10gggggggg
# 以逗号分隔的数字格式
"{:,}".format(10000000)  # 10,000,000
# 百分比格式
"{:.2%}".format(0.52)   # 52.00%
# 科学数字
"{:/2e}".format(1000000)    # 1.00e+06
# 进制转换格式，b, d, o, x分别是二进制、十进制、八进制和十六进制
"{:b}".format(10)       # 1010
```
