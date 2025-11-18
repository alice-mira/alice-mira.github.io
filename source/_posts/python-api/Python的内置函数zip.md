---
title: Python的内置函数zip
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 zip](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md)

Python 的内置函数 [`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 是一个非常有用的工具函数，用于将多个可迭代对象（如列表、元组等）中的元素按顺序打包成一个个元组，然后返回由这些元组组成的迭代器。其基本语法为：

```python
zip(*iterables)

```

其中，`iterables` 可以是多个可迭代对象，比如列表、元组、字符串等。[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 函数会将这些可迭代对象中相同索引位置的元素组合成一个元组，最终返回一个迭代器。

#### 主要特点

1. **并行迭代**：[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 可以同时遍历多个可迭代对象，非常适合在需要同时处理多个序列数据时使用。
2. **惰性计算**：[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 返回的是一个迭代器，而不是列表，只有在需要时才会生成数据，这在处理大数据集时能节省内存。
3. **长度匹配**：当输入的可迭代对象长度不一致时，[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 会以最短的可迭代对象为准，忽略多余的元素。

#### 示例

假设有两个列表：

```python
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 35]

```

使用 [`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 将它们组合：

```python
zipped = zip(names, ages)
print(list(zipped))  # 输出：[('Alice', 25), ('Bob', 30), ('Charlie', 35)]

```

#### 解压

可以使用 [`zip(*zipped)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 来解压数据：

```python
names_unzipped, ages_unzipped = zip(*zipped)
print(names_unzipped)  # 输出：('Alice', 'Bob', 'Charlie')
print(ages_unzipped)    # 输出：(25, 30, 35)

```

#### 应用场景

1. **数据配对**：将多个列表中的数据一一对应组合。
2. **并行处理**：在循环中同时处理多个序列数据。
3. **字典构造**：结合 [`dict()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md) 快速构造字典：  
```python  
person_dict = dict(zip(names, ages))  
print(person_dict)  # 输出：{'Alice': 25, 'Bob': 30, 'Charlie': 35}  
```

#### 注意事项

* 在 Python 2 中，[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 直接返回一个列表，而在 Python 3 中返回的是迭代器。如果需要列表，需显式转换为 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)。
* 如果输入的可迭代对象长度不同，[`zip()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.zip.md) 会以最短的为准，忽略多余的元素。如果需要以最长的为准，可以使用 `itertools.zip_longest()`。

---

> 《[Python 的内置函数 zip](https://xplanc.online/c1853585cbbef8090c0f3599eaa58e4fc23e6ff0ad041783f0fdbb97365a4a36)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/152422078)。