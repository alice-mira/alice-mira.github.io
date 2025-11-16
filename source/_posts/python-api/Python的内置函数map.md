---
title: Python的内置函数map
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 map](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md)

Python 的内置函数 [`map()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 是一个高阶函数，它允许对一个可迭代对象（如列表、元组等）的所有元素应用指定的函数，并返回一个 [`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 对象（可迭代对象）。其基本语法是：

```python
map(function, iterable, ...)

```

**主要特点：**

1. 惰性计算（Lazy Evaluation）：[`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 对象不会立即执行计算，只有在需要时才会真正处理数据
2. 多参数支持：可以同时处理多个可迭代对象
3. 函数式编程特性：配合 lambda 表达式使用尤为方便

**常见使用场景：**

1. [简单数值转换](https://xplanc.org/shift/?lang=python&code=bnVtYmVycyUyMCUzRCUyMCU1QjElMkMlMjAyJTJDJTIwMyUyQyUyMDQlNUQlMEFzcXVhcmVkJTIwJTNEJTIwbWFwKGxhbWJkYSUyMHglM0ElMjB4KioyJTJDJTIwbnVtYmVycyklMEFwcmludChsaXN0KHNxdWFyZWQpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QSU1QjElMkMlMjA0JTJDJTIwOSUyQyUyMDE2JTVE)：

```python
numbers = [1, 2, 3, 4]
squared = map(lambda x: x**2, numbers)
print(list(squared))  # 输出：[1, 4, 9, 16]

```

1. [类型转换](https://xplanc.org/shift/?lang=python&code=c3RyX251bWJlcnMlMjAlM0QlMjAlNUInMSclMkMlMjAnMiclMkMlMjAnMyclNUQlMEFpbnRfbnVtYmVycyUyMCUzRCUyMG1hcChpbnQlMkMlMjBzdHJfbnVtYmVycyklMEFwcmludChsaXN0KGludF9udW1iZXJzKSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUElNUIxJTJDJTIwMiUyQyUyMDMlNUQ%3D)：

```python
str_numbers = ['1', '2', '3']
int_numbers = map(int, str_numbers)
print(list(int_numbers))  # 输出：[1, 2, 3]

```

**注意事项：**

1. [`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 对象是迭代器，只能遍历一次。如果需要多次使用，应转换为列表
2. 当多个可迭代对象长度不一致时，以最短的对象为准
3. 在 Python 3 中返回的是 [`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 对象，而在 Python 2 中直接返回列表

**替代方案：**  
 对于简单场景，列表推导式通常更加直观：

```python
# 等价于 map(lambda x: x**2, numbers)
squared = [x**2 for x in numbers]

```

但在处理多个可迭代对象或需要复用函数时，[`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 仍然有其优势。

---

> 《[Python 的内置函数 map](https://xplanc.online/ddb09c20e4bb7a4d2558964b683f0743b304b267d2ea7fb3841a91b90e5291ce)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148937762)。