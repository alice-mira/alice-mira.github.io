---
title: Python的内置函数range
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 range](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)

## Python的内置函数range详解

[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)是Python中一个非常实用的内置函数，主要用于生成一个不可变的整数序列。它在循环和迭代操作中应用广泛。

### 基本语法

[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)函数有三种调用方式：

1. [`range(stop)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)：生成从0开始到stop-1的整数序列
2. [`range(start, stop)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)：生成从start开始到stop-1的整数序列
3. [`range(start, stop, step)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)：生成从start开始到stop-1的整数序列，步长为step

### 详细说明

#### 参数特点

* **start**：序列的起始值（包含），默认为0
* **stop**：序列的结束值（不包含）
* **step**：步长（可以为正数或负数），默认为1

#### 返回值

[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)函数返回的是一个[`range`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)对象，而不是列表。这个对象是**惰性求值**的，只有在需要时才计算值。如果需要列表，可以用[`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)转换：

```python
numbers = list(range(5))  # [0, 1, 2, 3, 4]

```

### 示例应用

#### [基础示例](https://xplanc.org/shift/?lang=python&code=JTIzJTIwJUU3JTk0JTlGJUU2JTg4JTkwMC00JUU3JTlBJTg0JUU1JUJBJThGJUU1JTg4JTk3JTBBZm9yJTIwaSUyMGluJTIwcmFuZ2UoNSklM0ElMEElMjAlMjAlMjAlMjBwcmludChpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMDAlMjAxJTIwMiUyMDMlMjA0JTBBJTBBJTIzJTIwJUU3JTk0JTlGJUU2JTg4JTkwMi01JUU3JTlBJTg0JUU1JUJBJThGJUU1JTg4JTk3JTBBZm9yJTIwaSUyMGluJTIwcmFuZ2UoMiUyQyUyMDYpJTNBJTBBJTIwJTIwJTIwJTIwcHJpbnQoaSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElM0ElMjAyJTIwMyUyMDQlMjA1JTBBJTBBJTIzJTIwJUU3JTk0JTlGJUU2JTg4JTkwMC0xMCVFNyU5QSU4NCVFNSU4MSVCNiVFNiU5NSVCMCVFNSVCQSU4RiVFNSU4OCU5NyUwQWZvciUyMGklMjBpbiUyMHJhbmdlKDAlMkMlMjAxMSUyQyUyMDIpJTNBJTBBJTIwJTIwJTIwJTIwcHJpbnQoaSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElM0ElMjAwJTIwMiUyMDQlMjA2JTIwOCUyMDEwJTBBJTBBJTIzJTIwJUU1JThGJThEJUU1JTkwJTkxJUU1JUJBJThGJUU1JTg4JTk3JTBBZm9yJTIwaSUyMGluJTIwcmFuZ2UoNSUyQyUyMDAlMkMlMjAtMSklM0ElMEElMjAlMjAlMjAlMjBwcmludChpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMDUlMjA0JTIwMyUyMDIlMjAx)

```python
# 生成0-4的序列
for i in range(5):
    print(i)  # 输出: 0 1 2 3 4

# 生成2-5的序列
for i in range(2, 6):
    print(i)  # 输出: 2 3 4 5

# 生成0-10的偶数序列
for i in range(0, 11, 2):
    print(i)  # 输出: 0 2 4 6 8 10

# 反向序列
for i in range(5, 0, -1):
    print(i)  # 输出: 5 4 3 2 1

```

#### 实际应用场景

1. **循环固定次数**：

```python
for _ in range(3):
    print("Hello")  # 打印3次Hello

```

1. **列表索引遍历**：

```python
fruits = ['apple', 'banana', 'cherry']
for i in range(len(fruits)):
    print(f"Index {i}: {fruits[i]}")

```

1. **数学运算序列**：

```python
squares = [x**2 for x in range(10)]  # 生成0-9的平方列表

```

1. **时间序列生成**：

```python
hours = list(range(0, 24, 3))  # [0, 3, 6, 9, 12, 15, 18, 21]

```

### 注意事项

1. [`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)生成的序列**不包含**结束值
2. 步长不能为0，否则会引发`ValueError`
3. 对于负步长，start应该大于stop
4. [`range`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)对象支持索引、切片等操作，但不支持修改
5. 相比直接生成列表，[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)更节省内存，特别是处理大范围时

### 性能优势

[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)相比直接生成列表的优势在于：

* 内存效率高：只存储start、stop和step值，不存储完整序列
* 计算效率高：只在需要时才计算当前值
* 支持无限序列（理论上）：虽然实际受限于系统资源

在Python 3中，[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)的这种"惰性"特性使其成为处理大范围数字序列的理想选择。

---

> 《[Python 的内置函数 range](https://xplanc.online/6ce967967a920caafb3cdbc59f153eaeabf547ce107e565ccf1faeec31d39ab3)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149102633)。