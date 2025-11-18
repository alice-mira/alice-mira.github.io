---
title: Python的内置函数isinstance
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 isinstance](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md)

Python 的内置函数 [`isinstance()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md) 用于判断一个对象是否属于某个类或类型，或者是否属于由这些类型组成的元组中的一个。它是 Python 中类型检查的重要工具，相比于 [`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 函数具有更灵活的类型检查能力。

其语法为：

```python
isinstance(object, classinfo)

```

其中：

* [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 是要检查的对象
* `classinfo` 可以是一个类型对象，或者由类型对象组成的元组

[`isinstance()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md) 的主要特点包括：

1. 支持继承关系检查：当 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 是 `classinfo` 的子类实例时也会返回 True
2. 返回布尔值：符合条件返回 True，否则返回 False

常见应用场景：

* 类型检查：验证输入参数的类型是否符合预期
* 多类型处理：处理可能属于多种类型的对象
* 继承关系验证：检查对象是否属于某个类或其子类

[示例](https://xplanc.org/shift/?lang=python&code=JTIzJTIwJUU1JTlGJUJBJUU2JTlDJUFDJUU3JUIxJUJCJUU1JTlFJThCJUU2JUEzJTgwJUU2JTlGJUE1JTBBbnVtJTIwJTNEJTIwNDIlMEFwcmludChpc2luc3RhbmNlKG51bSUyQyUyMGludCkpJTIwJTIwJTIzJTIwVHJ1ZSUwQSUwQSUyMyUyMCVFNyVCQiVBNyVFNiU4OSVCRiVFNSU4NSVCMyVFNyVCMyVCQiVFNiVBMyU4MCVFNiU5RiVBNSUwQWNsYXNzJTIwUGFyZW50JTNBJTIwcGFzcyUwQWNsYXNzJTIwQ2hpbGQoUGFyZW50KSUzQSUyMHBhc3MlMEFvYmolMjAlM0QlMjBDaGlsZCgpJTBBcHJpbnQoaXNpbnN0YW5jZShvYmolMkMlMjBQYXJlbnQpKSUyMCUyMCUyMyUyMFRydWUlMEElMEElMjMlMjAlRTUlQTQlOUElRTclQjElQkIlRTUlOUUlOEIlRTYlQTMlODAlRTYlOUYlQTUlMEF2YWx1ZSUyMCUzRCUyMDMuMTQlMEFwcmludChpc2luc3RhbmNlKHZhbHVlJTJDJTIwKGludCUyQyUyMGZsb2F0KSkpJTIwJTIwJTIzJTIwVHJ1ZSUwQSUwQSUyMyUyMCVFNCVCOCU4RSUyMHR5cGUoKSUyMCVFNyU5QSU4NCVFNSU4QyVCQSVFNSU4OCVBQiUwQXByaW50KGlzaW5zdGFuY2UoVHJ1ZSUyQyUyMGludCkpJTIwJTIwJTIzJTIwVHJ1ZSUyMCglRTUlOUIlQTAlRTQlQjglQkElMjBib29sJTIwJUU2JTk4JUFGJTIwaW50JTIwJUU3JTlBJTg0JUU1JUFEJTkwJUU3JUIxJUJCKSUwQXByaW50KHR5cGUoVHJ1ZSklMjAlM0QlM0QlMjBpbnQpJTIwJTIwJTIzJTIwRmFsc2U%3D)：

```python
# 基本类型检查
num = 42
print(isinstance(num, int))  # True

# 继承关系检查
class Parent: pass
class Child(Parent): pass
obj = Child()
print(isinstance(obj, Parent))  # True

# 多类型检查
value = 3.14
print(isinstance(value, (int, float)))  # True

# 与 type() 的区别
print(isinstance(True, int))  # True (因为 bool 是 int 的子类)
print(type(True) == int)  # False

```

注意事项：

* 对于抽象基类(ABC)的检查，通常使用 `collections.abc` 模块中的抽象基类
* 在 Python 3 中，类与类型已经统一，因此 [`isinstance()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md) 可以用于检查内置类型和自定义类
* 过度使用类型检查可能会影响代码的灵活性，在 Python 中更推荐"鸭子类型"的编程风格

---

> 《[Python 的内置函数 isinstance](https://xplanc.online/f3a0189088961c9cc667ee20b19337dc14913026ee25c63145613440433de3c4)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148857716)。