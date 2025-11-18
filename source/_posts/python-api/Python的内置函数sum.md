---
title: Python的内置函数sum
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 sum](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md)

Python 的内置函数 [`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md) 是一个用于计算可迭代对象中所有元素之和的高效工具。这个函数可以接受一个可迭代对象（如列表、元组、集合等）作为参数，并返回其中所有元素的总和。

#### 基本用法

```python
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)  # 返回 15

```

#### 可选参数

[`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md) 函数还接受一个可选的第二个参数 `start`，用于指定求和的初始值。默认情况下 `start` 为 0。

```python
numbers = [1, 2, 3]
total = sum(numbers, 10)  # 返回 16 (1+2+3+10)

```

#### 支持的数据类型

[`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md) 可以处理各种数值类型，包括：

* 整数 ([`int`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md))
* 浮点数 ([`float`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md))
* 复数 ([`complex`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.complex.md))
* 其他实现了 `__add__` 方法的对象

#### 注意事项

1. 不能直接对非数值类型的可迭代对象使用 [`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md)，除非这些对象实现了 `__add__` 方法。  
```python  
strings = ["a", "b", "c"]  
# sum(strings)  # 会抛出 TypeError  
```
2. 对于浮点数求和可能存在精度问题，可以使用 `math.fsum()` 获得更高精度的结果。

#### 应用场景

1. 计算列表总和：  
```python  
grades = [85, 90, 78, 92]  
total_score = sum(grades)  
```
2. 带初始值的累加：  
```python  
account_balances = [100.50, 250.75, 300.00]  
initial_balance = 500  
current_balance = sum(account_balances, initial_balance)  
```
3. 与其他函数结合使用：  
```python  
# 计算列表中偶数的和  
numbers = range(1, 11)  
even_sum = sum(x for x in numbers if x % 2 == 0)  
```

#### 性能考虑

[`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md) 是使用 C 实现的，对于大型数据集比手动循环累加更高效。在处理非常大的可迭代对象时，建议使用生成器表达式而非先创建完整列表：

```python
# 更高效的方式
total = sum(x for x in range(1000000))

```

[`sum()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sum.md) 是 Python 中简单但功能强大的内置函数，能够处理各种数值累加任务，是数据分析、科学计算等场景中的常用工具。

---

> 《[Python 的内置函数 sum](https://xplanc.online/23d0e1093db061f918c6116d3c9b1ebf776ed5e72b38c7815ee7f1399651202d)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/150185802)。