---
title: Python的内置函数repr
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 repr](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md)

Python 的内置函数 [`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 是一个非常重要的对象字符串表示函数，其主要功能是返回一个对象的"官方"字符串表示形式（通常称为"representation"）。这个字符串通常能够被 Python 解释器读取，并尽可能准确地重建该对象。

#### 详细特性：

1. **可重建性原则**：[`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 返回的字符串理论上应该能够通过 [`eval()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.eval.md) 函数重新构造出原对象
2. **与 [`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 的区别**：相比 [`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 函数返回的可读性字符串，[`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 更关注精确性和开发调试的需要
3. **内置对象的 repr**：Python 内置类型都有良好的 [`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 实现，比如：  
```python  
repr([1, 2, 3])  # 返回 '[1, 2, 3]'  
repr('hello')    # 返回 "'hello'"  
```

#### 使用场景：

1. **调试和开发**：在调试代码时查看变量的精确状态
2. **日志记录**：记录对象的详细信息
3. **交互式解释器**：Python REPL 环境使用 [`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 显示表达式结果

#### [自定义实现](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBQb2ludCUzQSUwQSUyMCUyMCUyMCUyMGRlZiUyMF9faW5pdF9fKHNlbGYlMkMlMjB4JTJDJTIweSklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLnglMjAlM0QlMjB4JTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwc2VsZi55JTIwJTNEJTIweSUwQSUyMCUyMCUyMCUyMCUwQSUyMCUyMCUyMCUyMGRlZiUyMF9fcmVwcl9fKHNlbGYpJTNBJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwcmV0dXJuJTIwZiUyMlBvaW50KCU3QnNlbGYueCU3RCUyQyUyMCU3QnNlbGYueSU3RCklMjIlMEElMEFwcmludChQb2ludCg1JTJDJTIwMTUpKQ%3D%3D)：

用户可以在自定义类中通过定义 `__repr__` 方法来实现对象的 [`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 行为：

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        return f"Point({self.x}, {self.y})"

```

#### 注意事项：

* 对于没有 `__repr__` 方法的对象，默认会返回类似 `<module 'sys' (built-in)>` 的信息
* 当 `__str__` 未定义时，[`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 会调用 `__repr__` 作为备用
* 字符串的 [`repr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.repr.md) 会包含引号，而 [`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 不会

---

> 《[Python 的内置函数 repr](https://xplanc.online/100b46d0a2bac85b1effb8f97749562ed8ae18ab950fd7aec4ec9060b3bf3a7d)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149125800)。