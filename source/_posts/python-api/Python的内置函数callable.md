---
title: Python的内置函数callable
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 callable](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.callable.md)

```python
def callable(obj):
    '''
    判断对象是否可调用

    :param obj: 一个代对象
    :return: 如果 obj 可以调用则返回 True，否则返回 False
    '''

```

Python 的内置函数 [`callable()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.callable.md) 用于检查一个对象是否可以被调用（即该对象是否能像函数一样被调用）。该函数返回一个布尔值，如果对象是可调用的则返回 `True`，否则返回 `False`。

### 可调用对象的类型

1. **函数**：包括内置函数、自定义函数和 lambda 表达式。
2. **方法**：类中定义的方法。
3. **类**：类本身是可调用的，因为调用类会创建一个实例。
4. **实现了 `__call__` 方法的对象**：如果一个类实现了 `__call__` 方法，其实例也可以被调用。

#### 不可调用对象的示例

* 基本数据类型（如 [`int`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md)、[`str`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md)、[`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 等）：  
```python  
  print(callable(42))       # 输出: False  
  print(callable("hello"))  # 输出: False  
  print(callable([1, 2, 3])) # 输出: False  
  ```  
```

### 应用场景

1. **动态调用检查**：在需要动态判断一个对象是否能被调用时，可以使用 [`callable()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.callable.md) 进行验证。
2. **插件或扩展系统**：在开发插件系统时，可以用 [`callable()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.callable.md) 检查插件是否提供了可调用的接口。
3. **装饰器**：某些装饰器可能需要检查被装饰的对象是否可调用。

---

> 《[Python 的内置函数 callable](https://xplanc.online/efc60258f4b2c9494f1b06ac097b2df37043fc567007ece947386e58e618ea7d)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148591676)。