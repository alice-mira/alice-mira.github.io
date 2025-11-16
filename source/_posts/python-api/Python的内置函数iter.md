---
title: Python的内置函数iter
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 iter](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.iter.md)

Python 的内置函数 [`iter()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.iter.md) 用于创建一个迭代器对象，它可以将可迭代对象（如列表、元组、字典、集合等）转换为迭代器，从而支持逐个访问元素的操作。

#### 基本语法

```python
iter(iterable, sentinel)

```

* **iterable**：必需参数，表示要转换为迭代器的可迭代对象（如列表、字符串等）。
* **sentinel**：可选参数，用于指定迭代停止的条件值（主要用于自定义迭代行为）。

#### 示例说明

1. **[基本用法](https://xplanc.org/shift/?lang=python&code=bnVtYmVycyUyMCUzRCUyMCU1QjElMkMlMjAyJTJDJTIwMyUyQyUyMDQlNUQlMEFudW1faXRlciUyMCUzRCUyMGl0ZXIobnVtYmVycyklMjAlMjAlMjMlMjAlRTglQkQlQUMlRTYlOEQlQTIlRTQlQjglQkElRTglQkYlQUQlRTQlQkIlQTMlRTUlOTklQTglMEFwcmludChuZXh0KG51bV9pdGVyKSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUExJTBBcHJpbnQobmV4dChudW1faXRlcikpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJUVGJUJDJTlBMg%3D%3D)**（无 `sentinel` 参数）

```python
numbers = [1, 2, 3, 4]
num_iter = iter(numbers)  # 转换为迭代器
print(next(num_iter))  # 输出：1
print(next(num_iter))  # 输出：2

```

1. **[文件逐行读取](https://xplanc.org/shift/?lang=python&code=d2l0aCUyMG9wZW4oX19maWxlX18lMkMlMjAncicpJTIwYXMlMjBmaWxlJTNBJTBBJTIwJTIwJTIwJTIwZmlsZV9pdGVyJTIwJTNEJTIwaXRlcihmaWxlLnJlYWRsaW5lJTJDJTIwJycpJTIwJTIwJTIzJTIwJUU5JTgwJTkwJUU4JUExJThDJUU4JUFGJUJCJUU1JThGJTk2JUVGJUJDJThDJUU3JTlCJUI0JUU1JTg4JUIwJUU5JTgxJTg3JUU1JTg4JUIwJUU3JUE5JUJBJUU1JUFEJTk3JUU3JUFDJUE2JUU0JUI4JUIyJTBBJTIwJTIwJTIwJTIwZm9yJTIwbGluZSUyMGluJTIwZmlsZV9pdGVyJTNBJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwcHJpbnQobGluZS5zdHJpcCgpKQ%3D%3D)**（常用于处理大文件）

```python
with open('data.txt', 'r') as file:
    file_iter = iter(file.readline, '')  # 逐行读取，直到遇到空字符串
    for line in file_iter:
        print(line.strip())

```

1. **[自定义迭代终止条件](https://xplanc.org/shift/?lang=python&code=aW1wb3J0JTIwcmFuZG9tJTBBZGVmJTIwZ2VuZXJhdGVfcmFuZG9tKCklM0ElMEElMjAlMjAlMjAlMjByZXR1cm4lMjByYW5kb20ucmFuZGludCgxJTJDJTIwMTApJTBBJTBBJTIzJTIwJUU1JUJEJTkzJUU3JTk0JTlGJUU2JTg4JTkwJUU3JTlBJTg0JUU5JTlBJThGJUU2JTlDJUJBJUU2JTk1JUIwJUU3JUFEJTg5JUU0JUJBJThFNSVFNiU5NyVCNiVFNSU4MSU5QyVFNiVBRCVBMiVFOCVCRiVBRCVFNCVCQiVBMyUwQXJhbmRvbV9pdGVyJTIwJTNEJTIwaXRlcihnZW5lcmF0ZV9yYW5kb20lMkMlMjA1KSUwQWZvciUyMG51bSUyMGluJTIwcmFuZG9tX2l0ZXIlM0ElMEElMjAlMjAlMjAlMjBwcmludChudW0p)**（使用 `sentinel`）

```python
import random
def generate_random():
    return random.randint(1, 10)

# 当生成的随机数等于5时停止迭代
random_iter = iter(generate_random, 5)
for num in random_iter:
    print(num)

```

#### 注意事项

* 如果没有更多元素可迭代，调用 [`next()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.next.md) 将抛出 `StopIteration` 异常。
* 字典迭代默认返回键（keys），可通过 [`dict.items()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md) 等方法获取键值对。
* 迭代器只能单向遍历，无法回退或重置，遍历结束后需重新创建迭代器。

#### 应用场景

* 处理大型数据集时节省内存（逐项读取而非一次性加载）。
* 实现自定义迭代逻辑（如条件终止）。
* 与生成器配合使用，支持惰性求值（lazy evaluation）。

---

> 《[Python 的内置函数 iter](https://xplanc.online/d14ac1ef41a99c3bd8ba249a1568830d38f97ccd18d349be8aebd1fa44a6241a)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148883092)。