---
title: Python的内置函数sorted
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 sorted](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md)

Python 的内置函数 [`sorted()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md) 是一个用于排序的可迭代对象的高阶函数，它接受一个可迭代对象作为输入，并返回一个新的已排序的列表。与列表的 `sort()` 方法不同，[`sorted()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md) 不会修改原始的可迭代对象，而是生成一个新的排序后的列表。

#### 基本用法

```python
sorted(iterable, key=None, reverse=False)

```

* **iterable**：需要排序的可迭代对象（如列表、元组、字符串等）
* **key**（可选）：指定一个函数作为排序的关键字，默认为 `None`
* **reverse**（可选）：布尔值，指定是否降序排序，默认为 `False`（升序）

#### 示例说明

##### 1\. 基本排序

```python
numbers = [5, 2, 9, 1, 5, 6]
sorted_numbers = sorted(numbers)
print(sorted_numbers)  # 输出：[1, 2, 5, 5, 6, 9]

```

##### 2\. 降序排序

```python
numbers = [5, 2, 9, 1, 5, 6]
sorted_numbers = sorted(numbers, reverse=True)
print(sorted_numbers)  # 输出：[9, 6, 5, 5, 2, 1]

```

##### 3\. 使用 key 参数

`key` 参数允许你指定一个函数，用于从每个元素中提取比较键。例如，对字符串列表按长度排序：

```python
words = ["apple", "banana", "cherry", "date"]
sorted_words = sorted(words, key=len)
print(sorted_words)  # 输出：['date', 'apple', 'banana', 'cherry']

```

##### 4\. 复杂对象排序

假设有一个学生列表，每个学生是一个字典：

```python
students = [
    {"name": "Alice", "age": 20},
    {"name": "Bob", "age": 18},
    {"name": "Charlie", "age": 22}
]
# 按年龄排序
sorted_students = sorted(students, key=lambda x: x["age"])
print(sorted_students)
# 输出：[{'name': 'Bob', 'age': 18}, {'name': 'Alice', 'age': 20}, {'name': 'Charlie', 'age': 22}]

```

#### 应用场景

1. **数据预处理**：在数据分析或机器学习中，经常需要对数据进行排序。
2. **展示排序结果**：在网页或应用中展示排序后的列表。
3. **算法实现**：某些算法（如合并排序）可能需要使用 [`sorted()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md) 作为辅助函数。

#### 注意事项

* 对于大型数据集，[`sorted()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md) 可能会消耗较多内存，因为它需要创建一个新的列表。
* 如果需要对列表进行原地排序，可以使用 [`list.sort()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 方法，它不会创建新的列表。

通过灵活使用 `key` 和 `reverse` 参数，[`sorted()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.sorted.md) 函数能够满足各种复杂的排序需求。

---

> 《[Python 的内置函数 sorted](https://xplanc.online/c910d38e01a34334d9342648ed1f7d2bc2bd98f4bb888c26e157a42c56ccaaf1)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149302683)。