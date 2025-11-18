---
title: Python的内置函数next
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 next](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md)

Python 的内置函数 [`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 是一个用于迭代器协议的重要函数，它能够从迭代器中获取下一个元素。[`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 函数的基本语法如下：

```python
next(iterator[, default])

```

其中：

* `iterator` 是一个可迭代对象（必须实现了 `__next__()` 方法的迭代器）
* `default` 是可选参数，当迭代器耗尽时返回该默认值，若不提供默认值且迭代器耗尽则会抛出 `StopIteration` 异常

使用示例：

1. 基本用法：

```python
numbers = iter([1, 2, 3])
print(next(numbers))  # 输出：1
print(next(numbers))  # 输出：2
print(next(numbers))  # 输出：3
print(next(numbers))  # 引发 StopIteration

```

1. 使用默认值：

```python
numbers = iter([1, 2])
print(next(numbers, 'end'))  # 输出：1
print(next(numbers, 'end'))  # 输出：2
print(next(numbers, 'end'))  # 输出：end

```

应用场景：

* 手动控制迭代过程
* 处理大型数据集时按需获取数据
* 实现自定义的迭代行为
* 与 [`iter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.iter.md) 函数配合使用来创建和操作迭代器

注意事项：

1. 对普通序列（如列表、元组）直接使用 [`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 会引发 TypeError，需要先用 [`iter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.iter.md) 转换为迭代器
2. 当迭代器耗尽时，如果不提供默认值则会抛出 `StopIteration` 异常
3. 在 for 循环中，Python 会自动处理 `StopIteration`，但直接使用 [`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 时需要手动处理

高级用法示例：

```python
with open('data.txt') as f:
    header = next(f)  # 获取文件第一行
    for line in f:    # 继续读取剩余内容
        process(line)

```

在 Python 3 中，[`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 实际上是调用迭代器的 `__next__()` 方法，这是 Python 迭代器协议的核心部分。

---

> 《[Python 的内置函数 next](https://xplanc.online/569b08b704aa4d6a8993076e1da98c0822a35c499a15ef833ed235f7640bbb52)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148985170)。