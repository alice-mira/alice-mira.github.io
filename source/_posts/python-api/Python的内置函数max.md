---
title: Python的内置函数max
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 max](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md)

Python 的内置函数 [`max()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md) 是一个用于返回可迭代对象中最大元素或多个参数中最大值的实用函数。它支持多种数据类型和灵活的调用方式，是 Python 编程中常用的工具之一。

#### 基本用法

1. **单个可迭代对象**：  
```python  
numbers = [3, 1, 4, 1, 5, 9, 2]  
print(max(numbers))  # 输出：9  
```
2. **多个参数**：  
```python  
print(max(3, 1, 4, 1, 5))  # 输出：5  
```

#### 关键参数

* `key`：指定一个单参数函数，用于从每个元素中提取比较键值  
```python  
words = ["apple", "banana", "cherry"]  
print(max(words, key=len))  # 输出："banana"（最长的字符串）  
```
* `default`：当可迭代对象为空时返回的默认值（仅适用于单可迭代对象调用）  
```python  
empty_list = []  
print(max(empty_list, default=0))  # 输出：0  
```

#### 支持的数据类型

[`max()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md) 可以处理：

* 数字（整数、浮点数）
* 字符串（按字典顺序比较）
* 元组、列表等序列
* 任何实现了 `__gt__()` 方法的对象

#### 特殊用法示例

1. **字典中值最大的键**：  
```python  
scores = {"Alice": 90, "Bob": 85, "Charlie": 95}  
print(max(scores, key=scores.get))  # 输出："Charlie"  
```
2. **自定义对象比较**：  
```python  
class Person:  
    def __init__(self, name, age):  
        self.name = name  
        self.age = age  
      
    def __gt__(self, other):  
        return self.age > other.age  
people = [Person("Alice", 30), Person("Bob", 25)]  
print(max(people).name)  # 输出："Alice"  
```

#### 注意事项

* 当比较的元素类型不同时（如数字和字符串），会引发 `TypeError`
* 对于空的可迭代对象且未提供 `default` 参数时，会引发 `ValueError`
* 在 Python 3 中，[`max()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md) 不能直接在字典上使用，需要使用 [`max(dict.keys())`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md) 或 [`max(dict.values())`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md)

[`max()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.max.md) 函数在数据分析、算法实现和日常编程任务中都有广泛应用，熟练掌握它可以提高代码的简洁性和效率。

---

> 《[Python 的内置函数 max](https://xplanc.online/07583d44eb6f6931f9707f11feec12df0f6294737a3c351e73042358267c5af7)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148964312)。