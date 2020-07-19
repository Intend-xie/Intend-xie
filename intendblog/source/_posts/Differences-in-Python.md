---
title: Python2.7和3.7区别
date: 2020-07-14 18:50:13
tags: Python
---

此文仅是本人学习笔记。
文章来源：https://www.cnblogs.com/sqm724/p/13294061.html?utm_source=tuicool

**区别一:print语法使用**

Python2.7  print语法使用  >>> print "Hello Python"    
Python3.7  print语法使用  >>> print("Hello Python")

例子:在Python 3.7.0使用双引号触发SyntaxError异常机制 提示Did you mean 
```javascript
print "Hello Python3.7"

print("Hello Python3.7") 
```
print 换行和不换行区别
python 2.7 print 不换行使用","即可
python 3.7 print 不换行使用end=""
```javascript
x = "a"
y = "b"

print(x)
print(y,end="") 
```

**区别二: raw_input()和input()**

Python 2.7  raw_input()  input() 都存在 可使用    raw_input()接收字符串string  input()接收数字int /flot.
Python 3.7  raw_input()不存在  仅存在input()   两者合并  接收任意格式 返回string

**区别三: 函数cmp()**

python 2.7   cmp(x,y)函数用于比较2个对象，如果 x < y 返回 -1, 如果 x == y 返回 0, 如果 x > y 返回 1
python3.7    cmp()已经不存在了,如果你需要实现比较功能，需要引入 operator 模块，适合任何对象
```javascript
import operator
operator.eq('hello', 'name');   //False
operator.eq('hello', 'hello');   //True
```

**区别四:string 字母 大小写字符串**

string.letters:包含所有字母（大写或小写）的字符串
Python 3.0中，string.ascii_letters.


