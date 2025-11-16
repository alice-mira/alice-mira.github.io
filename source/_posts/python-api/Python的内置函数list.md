---
title: Python的内置函数list
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 list](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)

Python 的内置函数 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 是用于创建列表对象的构造函数，它是 Python 中最常用的数据结构之一。

```python
def list(x=None):
    '''
    类型转换为 list

    :param x: 一个变量
    :return: 转换为 list 后的值
    '''

```

#### 详细功能说明

1. **创建空列表**：  
   * 最简单用法是不带任何参数调用 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)  
   * 示例：[`my_list = list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 创建一个空列表，等同于 `my_list = []`
2. **从可迭代对象创建列表**：  
   * 可以接受任何可迭代对象作为参数（字符串、元组、字典、集合等）  
   * 示例：[`list("hello")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 返回 `['h', 'e', 'l', 'l', 'o']`  
   * 示例：[`list((1,2,3))`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 返回 `[1, 2, 3]`  
   * 示例：[`list({'a':1, 'b':2})`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 返回 `['a', 'b']`
3. **类型转换**：  
   * 常用于将其他序列类型转换为列表  
   * 在处理字符串时特别有用，可以方便地进行字符级操作
4. **对象方法**：  
   * 创建的列表对象具有丰富的内置方法：  
         * `append()`, `extend()` \- 添加元素  
         * `pop()`, `remove()` \- 删除元素  
         * `sort()`, `reverse()` \- 排序操作  
         * `index()`, `count()` \- 查询操作

#### 实际应用场景

1. **数据处理**：  
   * 将字符串转换为字符列表进行文本处理  
   * 将生成器对象转换为可多次遍历的列表
2. **API开发**：  
   * 将数据库查询结果（通常是元组）转换为更易操作的列表
3. **算法实现**：  
   * 将其他数据结构转换为列表以利用列表的各种方法

#### 注意事项

* [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 是浅拷贝操作，对新列表元素的修改可能会影响原可迭代对象
* 对于大型数据，直接使用列表推导式可能比 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 更高效
* Python 3 中 [`list()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 不再支持多个参数，必须传入单个可迭代对象

#### 性能特点

* 时间复杂度：O(n)，n 是可迭代对象的长度
* 空间复杂度：O(n)，需要为新列表分配内存

#### [代码示例](https://xplanc.org/shift/?lang=python&code=JTIzJTIwJUU1JTg4JTlCJUU1JUJCJUJBJUU0JUI4JThEJUU1JTkwJThDJUU3JUIxJUJCJUU1JTlFJThCJUU3JTlBJTg0JUU1JTg4JTk3JUU4JUExJUE4JTBBZW1wdHklMjAlM0QlMjBsaXN0KCklMEFjaGFycyUyMCUzRCUyMGxpc3QoJTIyUHl0aG9uJTIyKSUwQW51bWJlcnMlMjAlM0QlMjBsaXN0KHJhbmdlKDUpKSUwQW1peGVkJTIwJTNEJTIwbGlzdCglNUIxJTJDJTIwJTIyYSUyMiUyQyUyMFRydWUlNUQpJTBBJTBBJTIzJTIwJUU1JUFEJTk3JUU1JTg1JUI4JUU4JUJEJUFDJUU2JThEJUEyJUU3JUE0JUJBJUU0JUJFJThCJTBBZGljdF90b19saXN0JTIwJTNEJTIwbGlzdCglN0InbmFtZSclM0ElMjAnQWxpY2UnJTJDJTIwJ2FnZSclM0ElMjAyNSU3RCklMjAlMjAlMjMlMjAlNUInbmFtZSclMkMlMjAnYWdlJyU1RCUwQXByaW50KGRpY3RfdG9fbGlzdCklMEElMEElMjMlMjAlRTQlQjglOEUlRTUlODglOTclRTglQTElQTglRTYlOEUlQTglRTUlQUYlQkMlRTUlQkMlOEYlRTUlQUYlQjklRTYlQUYlOTQlMEFzcXVhcmVzMSUyMCUzRCUyMGxpc3QobWFwKGxhbWJkYSUyMHglM0ElMjB4KioyJTJDJTIwcmFuZ2UoMTApKSklMEFzcXVhcmVzMiUyMCUzRCUyMCU1QngqKjIlMjBmb3IlMjB4JTIwaW4lMjByYW5nZSgxMCklNUQlMjAlMjAlMjMlMjAlRTYlOUIlQjQlRTYlOEUlQTglRTglOEQlOTAlRTclOUElODQlRTYlOTYlQjklRTUlQkMlOEYlMEFwcmludChzcXVhcmVzMSUyQyUyMHNxdWFyZXMyKQ%3D%3D)

```python
# 创建不同类型的列表
empty = list()
chars = list("Python")
numbers = list(range(5))
mixed = list([1, "a", True])

# 字典转换示例
dict_to_list = list({'name': 'Alice', 'age': 25})  # ['name', 'age']

# 与列表推导式对比
squares1 = list(map(lambda x: x**2, range(10)))
squares2 = [x**2 for x in range(10)]  # 更推荐的方式

```

---

> 《[Python 的内置函数 list](https://xplanc.online/a5b2431274a7e1e59f8479b27b79b582e6b5e38a417bab4d886cf0d2e6e9931d)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148910537)。