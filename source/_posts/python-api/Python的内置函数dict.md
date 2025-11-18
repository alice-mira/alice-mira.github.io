---
title: Python的内置函数dict
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 dict](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md)

Python 的内置函数 [`dict`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md) 是用于创建字典对象的构造函数。字典是 Python 中最常用的数据结构之一，它采用键值对（key-value pairs）的形式存储数据，提供高效的数据查询能力。

```python
class dict(**kwarg):
    '''
    类型转换为 dict

    :param kwarg: 键值对
    :return: 转换为 dict 后的值
    '''

```

### 示例

```python
person = dict(name='Alice', age=25, city='New York')
# 等同于
person = {'name': 'Alice', 'age': 25, 'city': 'New York'}

```

### 注意事项

* 字典会消耗较多内存
* 对于小型数据集，有时 [`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 或 [`tuple`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md) 可能更高效

---

> 《[Python 的内置函数 dict](https://xplanc.online/9b18305e66dd5971363083f39808e71c13baf78422571eed4449a7eee6e5cbf1)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148645109)。