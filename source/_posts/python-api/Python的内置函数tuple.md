---
title: Python的内置函数tuple
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 tuple](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md)

Python 的内置函数 [`tuple()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md) 用于创建一个不可变的序列（元组）。以下是关于 [`tuple()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md) 函数的详细说明：

#### 功能描述

[`tuple()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md) 函数可以将可迭代对象（如列表、字符串、集合等）转换为元组。如果调用时不传入参数，则返回一个空元组。

#### 语法

```python
tuple(iterable)

```

* **iterable**（可选）：任何可迭代对象（如列表、字符串、字典等）。如果未提供，则返回空元组 `()`。

#### 返回值

返回一个包含输入可迭代对象元素的元组。元组是不可变的，创建后不能修改。

#### 示例

1. **从列表创建元组**：  
```python  
list_data = [1, 2, 3]  
tuple_data = tuple(list_data)  
print(tuple_data)  # 输出：(1, 2, 3)  
```
2. **从字符串创建元组**：  
```python  
string_data = "hello"  
tuple_data = tuple(string_data)  
print(tuple_data)  # 输出：('h', 'e', 'l', 'l', 'o')  
```
3. **从字典创建元组**（默认转换为键的元组）：  
```python  
dict_data = {'a': 1, 'b': 2}  
tuple_data = tuple(dict_data)  
print(tuple_data)  # 输出：('a', 'b')  
```
4. **空元组**：  
```python  
empty_tuple = tuple()  
print(empty_tuple)  # 输出：()  
```
5. **从集合创建元组**：  
```python  
set_data = {1, 2, 3}  
tuple_data = tuple(set_data)  
print(tuple_data)  # 输出：(1, 2, 3)（顺序可能不同）  
```

#### 注意事项

* 元组是不可变的，创建后无法修改其内容（如添加、删除或更改元素）。
* 如果传入不可迭代的对象（如整数、布尔值等），会抛出 `TypeError`。
* 元组比列表更轻量，适合存储不需要修改的数据。

#### 应用场景

* 存储固定数据（如配置项、常量集合）。
* 作为字典的键（因为元组是不可变的，而列表不能作为字典的键）。
* 函数返回多个值时（实际上返回的是一个元组）。

#### 效率说明

元组的创建和访问速度比列表快，适合用于大量数据的只读场景。

---

> 《[Python 的内置函数 tuple](https://xplanc.online/b732f5a466cfa2e55f621b7263ed1b7b9a0237f643469d89c48cdaed05a20272)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/151980635)。