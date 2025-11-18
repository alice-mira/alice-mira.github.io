---
title: Python的内置函数hash
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 hash](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hash.md)

Python 的内置函数 [`hash()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hash.md) 是一个非常有用的工具函数，主要用于获取对象的哈希值。哈希值是一个固定长度的整数，代表该对象的唯一标识。在 Python 中，[`hash()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hash.md) 函数常用于字典键值、集合元素等场景，因为这些数据结构内部依赖哈希值来快速查找和比较对象。

#### 1\. **基本用法**

* [`hash()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hash.md) 函数接受一个对象作为参数，返回该对象的哈希值。
* 示例：  
```python  
print(hash("hello"))  # 输出字符串 "hello" 的哈希值  
print(hash(123))      # 输出整数 123 的哈希值  
```

#### 2\. **哈希值的特性**

* **不可变对象**：只有不可变对象（如字符串、元组、数字等）才能被哈希。如果尝试哈希可变对象（如列表、字典），会引发 `TypeError`。  
   * 示例：  
   ```python  
   hash([1, 2, 3])  # TypeError: unhashable type: 'list'  
   ```
* **一致性**：在同一个 Python 进程中，同一对象的哈希值保持不变。
* **不同对象可能相同**：不同对象可能有相同的哈希值（哈希碰撞），但概率较低。

#### 3\. **应用场景**

* **字典键值**：字典的键必须是可哈希的，因为 Python 使用哈希值快速定位键值对。  
   * 示例：  
   ```python  
   d = {}  
   d["key"] = "value"  # "key" 必须是可哈希的  
   ```
* **集合元素**：集合存储唯一元素，依赖哈希值判断元素是否重复。  
   * 示例：  
   ```python  
   s = {1, 2, 3}  # 集合中的元素必须是可哈希的  
   ```

#### 4\. **自定义对象的哈希**

* 如果[自定义类](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBQZXJzb24lM0ElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2luaXRfXyhzZWxmJTJDJTIwbmFtZSUyQyUyMGFnZSklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLm5hbWUlMjAlM0QlMjBuYW1lJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwc2VsZi5hZ2UlMjAlM0QlMjBhZ2UlMEElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2hhc2hfXyhzZWxmKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHJldHVybiUyMGhhc2goKHNlbGYubmFtZSUyQyUyMHNlbGYuYWdlKSklMjAlMjAlMjMlMjAlRTUlOUYlQkElRTQlQkElOEUlRTUlODUlODMlRTclQkIlODQlRTclOTQlOUYlRTYlODglOTAlRTUlOTMlODglRTUlQjglOEMlRTUlODAlQkMlMEElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2VxX18oc2VsZiUyQyUyMG90aGVyKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHJldHVybiUyMChzZWxmLm5hbWUlMkMlMjBzZWxmLmFnZSklMjAlM0QlM0QlMjAob3RoZXIubmFtZSUyQyUyMG90aGVyLmFnZSklMEElMEFwJTIwJTNEJTIwUGVyc29uKCUyMkFsaWNlJTIyJTJDJTIwMjUpJTBBcHJpbnQoaGFzaChwKSk%3D)需要支持哈希，可以重写 `__hash__()` 方法。通常还需要重写 `__eq__()` 方法以确保哈希一致性。  
   * 示例：  
   ```python  
   class Person:  
       def __init__(self, name, age):  
           self.name = name  
           self.age = age  
       def __hash__(self):  
           return hash((self.name, self.age))  # 基于元组生成哈希值  
       def __eq__(self, other):  
           return (self.name, self.age) == (other.name, other.age)  
   p = Person("Alice", 25)  
   print(hash(p))  
   ```

#### 5\. **注意事项**

* 哈希值在不同 Python 版本或不同机器上可能不同（如 Python 3.3+ 引入了随机哈希种子以防止攻击）。
* 哈希值不保证唯一性，仅用于快速比较和查找。

[`hash()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hash.md) 函数是 Python 中高效数据操作的重要工具，合理利用可以显著提升程序性能。

---

> 《[Python 的内置函数 hash](https://xplanc.online/36187cab37f86aa7965c9a12bb14febb328ba1248081991c5d272bc77c96add7)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148816890)。