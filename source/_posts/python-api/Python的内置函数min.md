---
title: Python的内置函数min
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 min](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.min.md)  
 Python 的内置函数 [`min()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.min.md) 是一个非常有用的工具函数，用于返回给定参数中的最小值。这个函数可以接受两种形式的参数：

1. **多个单独的参数**  
```python  
min(a, b, c, ...)  
```  
它会返回这些参数中的最小值。
2. **一个可迭代对象（如列表、元组、集合等）**  
```python  
min(iterable, *[, key, default])  
```  
它会遍历可迭代对象，并返回其中的最小值。

#### 参数说明：

* **iterable**：必须是一个可迭代对象（如列表、元组、字符串等）。
* **key**（可选）：用于指定一个函数，该函数作用于可迭代对象的每个元素，并依据该函数的返回值进行比较。
* **default**（可选）：如果可迭代对象为空，则返回该默认值。如果不提供 `default` 且可迭代对象为空，则会抛出 `ValueError`。

#### 示例：

1. **基本用法**  
```python  
print(min(1, 2, 3))        # 输出：1  
print(min([5, 2, 9, 4]))   # 输出：2  
```
2. **使用 `key` 参数**  
```python  
words = ["apple", "banana", "cherry"]  
print(min(words, key=lambda x: len(x)))  # 输出："apple"（最短的单词）  
```
3. **处理空可迭代对象**  
```python  
empty_list = []  
print(min(empty_list, default="No elements"))  # 输出："No elements"  
```
4. **字符串比较**  
```python  
print(min("Python"))  # 输出："P"（按 ASCII 码比较）  
```

#### 注意事项：

* 如果参数类型不同（如比较数字和字符串），[`min()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.min.md) 可能会抛出 `TypeError`。

[`min()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.min.md) 在数据分析、算法优化、查找最小值等场景中非常实用，是 Python 编程中的基础工具之一。

---

> 《[Python 的内置函数 min](https://xplanc.online/371b121a2d7e284a58a00cd581c18ca16dc3c6588744b4bb539c8545565842c7)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148985144)。