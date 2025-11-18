---
title: Python的内置函数filter
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---
[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 filter](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md)

Python 的内建函数 [`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 是一个非常有用的高阶函数，它用于对可迭代对象进行筛选过滤。它的基本工作原理是根据指定的函数条件，从输入的可迭代对象中筛选出符合条件的元素，返回一个迭代器对象。

```python
def filter(fn, iterable):
    '''
    过滤数据

    :param fn: 回调函数，返回 True 是元素保留，返回 False 时元素去除
    :param iterable: 要过滤的可迭代对象
    :return: 过滤后的可迭代对象
    '''

```

#### 详细说明

[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 函数的语法格式为：

```python
filter(function, iterable)

```

其中：

* `function` 是筛选条件函数，当该参数为 `None` 时，[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 会自动过滤掉可迭代对象中值为 `False` 的元素
* `iterable` 是待处理的可迭代对象，如列表、元组等

#### 工作原理

[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 会遍历 `iterable` 中的每个元素，并调用 `function` 函数进行测试：

1. 对于每个元素 `x`，计算 `function(x)`
2. 如果返回值为 `True`，则保留该元素
3. 如果返回值为 `False`，则过滤掉该元素

最终返回一个包含所有保留元素的迭代器对象。如果需要列表形式的结果，可以使用 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 进行转换。

#### 示例应用

##### 示例1：[过滤奇数](https://xplanc.org/shift/index.html?lang=python&code=bnVtYmVycyUyMCUzRCUyMCU1QjElMkMlMjAyJTJDJTIwMyUyQyUyMDQlMkMlMjA1JTJDJTIwNiU1RCUwQWV2ZW5fbnVtYmVycyUyMCUzRCUyMGZpbHRlcihsYW1iZGElMjB4JTNBJTIweCUyMCUyNSUyMDIlMjAlM0QlM0QlMjAwJTJDJTIwbnVtYmVycyklMEFwcmludChsaXN0KGV2ZW5fbnVtYmVycykpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJUVGJUJDJTlBJTVCMiUyQyUyMDQlMkMlMjA2JTVE)

```python
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = filter(lambda x: x % 2 == 0, numbers)
print(list(even_numbers))  # 输出：[2, 4, 6]

```

##### 示例2：[过滤空字符串](https://xplanc.org/shift/index.html?lang=python&code=c3RyaW5ncyUyMCUzRCUyMCU1QiUyMmhlbGxvJTIyJTJDJTIwJTIyJTIyJTJDJTIwJTIyd29ybGQlMjIlMkMlMjAlMjIlMjIlMkMlMjAlMjJweXRob24lMjIlNUQlMEFub25fZW1wdHklMjAlM0QlMjBmaWx0ZXIoTm9uZSUyQyUyMHN0cmluZ3MpJTBBcHJpbnQobGlzdChub25fZW1wdHkpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QSU1QidoZWxsbyclMkMlMjAnd29ybGQnJTJDJTIwJ3B5dGhvbiclNUQ%3D)

```python
strings = ["hello", "", "world", "", "python"]
non_empty = filter(None, strings)
print(list(non_empty))  # 输出：['hello', 'world', 'python']

```

##### 示例3：[使用自定义函数过滤](https://xplanc.org/shift/index.html?lang=python&code=ZGVmJTIwaXNfcG9zaXRpdmUobnVtKSUzQSUwQSUyMCUyMCUyMCUyMHJldHVybiUyMG51bSUyMCUzRSUyMDAlMEElMEFudW1iZXJzJTIwJTNEJTIwJTVCLTUlMkMlMjAtMyUyQyUyMDAlMkMlMjAyJTJDJTIwNCU1RCUwQXBvc2l0aXZlcyUyMCUzRCUyMGZpbHRlcihpc19wb3NpdGl2ZSUyQyUyMG51bWJlcnMpJTBBcHJpbnQobGlzdChwb3NpdGl2ZXMpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QSU1QjIlMkMlMjA0JTVE)

```python
def is_positive(num):
    return num > 0

numbers = [-5, -3, 0, 2, 4]
positives = filter(is_positive, numbers)
print(list(positives))  # 输出：[2, 4]

```

#### 注意事项

1. [`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 返回的是迭代器而不是列表，如果需要列表必须显式转换
2. 与列表推导式相比，[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 在可读性上有时不如列表推导式清晰
3. 当过滤条件简单时，使用 [`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 结合 `lambda` 会更简洁
4. 在 Python 3 中，[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 返回的是过滤器对象，而在 Python 2 中返回的是列表

#### 性能考虑

[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 的执行效率与列表推导式相当，但对于大型数据集，[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 可能更节省内存，因为它返回的是迭代器而不是完整的列表。在处理大数据集时，如果需要节省内存，[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 是更好的选择。

[`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 函数常与其他函数式编程工具如 [`map()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md)、`reduce()` 配合使用，可以构建出简洁高效的数据处理管道。这种组合方式遵循"数据转换流水线"的设计模式，每个函数专注于完成一个特定的数据处理任务：

1. [`filter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 负责数据筛选  
   * 示例：从列表中筛选出偶数  
```python  
numbers = [1, 2, 3, 4, 5, 6]  
even_numbers = filter(lambda x: x % 2 == 0, numbers)  
```
2. [`map()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md) 负责数据转换  
   * 接上例，将筛选出的偶数平方  
```python  
squared_evens = map(lambda x: x**2, even_numbers)  
```
3. `reduce()` 负责数据聚合  
   * 最后计算平方后的偶数和  
```python  
from functools import reduce  
sum_squared = reduce(lambda x, y: x + y, squared_evens)  
```

典型应用场景包括：

* 数据清洗流程：先过滤无效数据，再转换格式，最后汇总统计
* 日志分析：筛选特定级别的日志，提取关键信息，计算指标
* 电商数据处理：过滤已下架商品，转换价格格式，计算总销售额

这种组合的优势在于：

1. 代码可读性强，每个步骤意图明确
2. 内存效率高，生成器特性避免中间数据存储
3. 易于维护和扩展，可以灵活调整处理步骤顺序

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148704122)。