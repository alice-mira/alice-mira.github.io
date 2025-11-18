---
title: Python的内置函数enumerate
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 enumerate](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.enumerate.md)  
 Python 的内置函数 enumerate 是一个非常有用的工具函数，主要用于在遍历序列（如列表、元组或字符串）时，同时获取元素的索引和值。

基本语法如下：

```python
enumerate(iterable, start=0)

```

其中：

* `iterable` 表示任何可迭代对象
* `start` 是可选参数，指定索引的起始值，默认为 0

使用示例：

```python
fruits = ['apple', 'banana', 'orange']
for index, fruit in enumerate(fruits):
    print(index, fruit)

```

[运行](https://xplanc.org/shift/?lang=python&code=ZnJ1aXRzJTIwJTNEJTIwJTVCJ2FwcGxlJyUyQyUyMCdiYW5hbmEnJTJDJTIwJ29yYW5nZSclNUQlMEFmb3IlMjBpbmRleCUyQyUyMGZydWl0JTIwaW4lMjBlbnVtZXJhdGUoZnJ1aXRzKSUzQSUwQSUyMCUyMCUyMCUyMHByaW50KGluZGV4JTJDJTIwZnJ1aXQp)结果：

```txt
0 apple
1 banana
2 orange

```

---

> 《[Python 的内置函数 enumerate](https://xplanc.online/6a6802258275e127e1c7f9f6fc2a687a33fdf9061b5940d16953c5d76acd199f)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148679773)。