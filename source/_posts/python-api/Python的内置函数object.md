---
title: Python的内置函数object
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 object](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)

Python 的内置函数 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 是 Python 中最基础的类，它是所有类的基类。在 Python 中，所有的类都直接或间接地继承自 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类。[`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类提供了一些默认的方法和属性，这些方法和属性可以被所有 Python 对象使用。

#### 基本特性

1. **继承关系**：所有 Python 类默认都继承自 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)。例如，定义一个空类时，实际上它已经隐式地继承了 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类。  
```python  
class MyClass:  
    pass  
# 等同于  
class MyClass(object):  
    pass  
```
2. **默认方法**：[`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类提供了一些默认方法，如 `__str__`, `__repr__`, `__eq__` 等。这些方法可以在子类中被重写以实现自定义行为。  
   * `__str__`: 返回对象的字符串表示，通常用于 [`print()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 函数。  
   * `__repr__`: 返回对象的官方字符串表示，通常用于调试。  
   * `__eq__`: 定义对象的相等性比较。
3. **实例创建**：[`object()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 可以直接创建一个空对象实例。虽然这个实例没有自定义的属性和方法，但它拥有 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类提供的基本功能。  
```python  
obj = object()  
print(obj)  # 输出: <object object at 0x...>  
```

#### 应用场景

1. **作为基类**：在自定义类时，[`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 可以作为基类，用于定义新的数据类型。例如：  
```python  
class Person(object):  
    def __init__(self, name):  
        self.name = name  
    def __str__(self):  
        return f"Person: {self.name}"  
```
2. **类型检查**：[`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 是所有类的基类，因此可以用它来进行类型检查。例如：  
```python  
isinstance(42, object)  # 返回 True  
isinstance("hello", object)  # 返回 True  
```
3. **默认行为**：当需要创建一个没有任何自定义行为的对象时，可以直接使用 [`object()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)。这在某些特殊情况下可能有用，比如作为占位符或默认值。  
```python  
default_obj = object()  
```

#### 示例代码

以下是一个[简单的示例](https://xplanc.org/shift/?lang=python&code=JTIzJTIwJUU1JUFFJTlBJUU0JUI5JTg5JUU0JUI4JTgwJUU0JUI4JUFBJUU3JUJCJUE3JUU2JTg5JUJGJUU4JTg3JUFBJTIwb2JqZWN0JTIwJUU3JTlBJTg0JUU3JUIxJUJCJTBBY2xhc3MlMjBBbmltYWwob2JqZWN0KSUzQSUwQSUyMCUyMCUyMCUyMGRlZiUyMF9faW5pdF9fKHNlbGYlMkMlMjBuYW1lKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHNlbGYubmFtZSUyMCUzRCUyMG5hbWUlMEElMEElMjAlMjAlMjAlMjBkZWYlMjBfX3N0cl9fKHNlbGYpJTNBJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwcmV0dXJuJTIwZiUyMkFuaW1hbCUzQSUyMCU3QnNlbGYubmFtZSU3RCUyMiUwQSUwQSUyMyUyMCVFNSU4OCU5QiVFNSVCQiVCQSVFNSVBRSU5RSVFNCVCRSU4QiUwQWRvZyUyMCUzRCUyMEFuaW1hbCglMjJEb2clMjIpJTBBcHJpbnQoZG9nKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMEFuaW1hbCUzQSUyMERvZyUwQSUwQSUyMyUyMCVFNiVBMyU4MCVFNiU5RiVBNSVFNyVCQiVBNyVFNiU4OSVCRiVFNSU4NSVCMyVFNyVCMyVCQiUwQXByaW50KGlzaW5zdGFuY2UoZG9nJTJDJTIwb2JqZWN0KSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElM0ElMjBUcnVlJTBBcHJpbnQoaXNzdWJjbGFzcyhBbmltYWwlMkMlMjBvYmplY3QpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMFRydWU%3D)，展示如何使用 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类和自定义类：

```python
# 定义一个继承自 object 的类
class Animal(object):
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Animal: {self.name}"

# 创建实例
dog = Animal("Dog")
print(dog)  # 输出: Animal: Dog

# 检查继承关系
print(isinstance(dog, object))  # 输出: True
print(issubclass(Animal, object))  # 输出: True

```

#### 注意事项

* 在 Python 3 中，所有类默认继承自 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)，因此不需要显式地写出 [`(object)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)。但在 Python 2 中，如果不显式继承 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)，创建的是旧式类（old-style class），这会影响到方法解析顺序（MRO）和一些内置方法的行为。
* [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 实例本身没有 `__dict__` 属性，因此不能动态添加属性。如果需要动态添加属性，可以继承 [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 并定义 `__dict__` 或使用其他方式。

总之，[`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 类是 Python 类体系的根基，理解它的作用和特性对于掌握 Python 面向对象编程至关重要。

---

> 《[Python 的内置函数 object](https://xplanc.online/31f46e33ac5c38abb85687908fc96a99cb62b5e6f8d3ddcef74a14b6a255b825)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149032888)。