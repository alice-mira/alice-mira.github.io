---
title: Python的内置函数 any
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 any](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.hide/EX.any.md)

any()函数用于判断可迭代对象中是否存在至少一个为True的元素，它就像是一个"是否存在"的快速检测器。想象一下，当你需要检查列表中是否有元素满足某个条件时，any()可以让你用一行代码就搞定原本需要多行循环才能实现的功能。接下来，让我们一起探索这个函数的用法、原理和实际应用场景吧！

anext 的函数原型如下：

```python
def any(iterable):
    '''
    判断可迭代对象内容是否存在真值

    :param iterable: 一个可迭代对象
    :return: 如果 iterable 中存在真值则返回 True，否则返回 False；如果 iterable 是空的，返回 False
    '''

```

### 示例

[在线运行](https://xplanc.org/shift/#lang=python&input=&code=cHJpbnQoYW55KCU1QiU1RCkpJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIzJTIwJUU3JUE5JUJBJUU3JTlBJTg0JUU1JThGJUFGJUU4JUJGJUFEJUU0JUJCJUEzJUU1JUFGJUI5JUU4JUIxJUExJUU4JUJGJTk0JUU1JTlCJTlFJTIwRmFsc2UlMEFwcmludChhbnkocmFuZ2UoMTApKSklMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjMlMjAwLi4uOSUwQXByaW50KGFueSglNUIwJTIwZm9yJTIwXyUyMGluJTIwcmFuZ2UoMCklNUQpKSUyMCUyMCUyMCUyMyUyMDAuLi4w)

```python
print(any([]))                      # 空的可迭代对象返回 False
print(any(range(10)))               # 0...9
print(any([0 for _ in range(0)]))   # 0...0

```

any()的精髓在于它提供了一种简洁的方式来检查可迭代对象中是否存在满足条件的元素，这不仅能减少代码量，还能提高代码的可读性。

在实际编程中，当你遇到需要判断"是否存在"、"是否至少有一个"这类问题时，不妨考虑使用any()函数。它和列表推导式、生成器表达式结合使用时尤其强大。

---

> 《[Python 的内置函数 any](https://xplanc.online/14587b22bd659b82b57d87cea513f18de7535719c42228b4080dce30532c8eea)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148542127)。