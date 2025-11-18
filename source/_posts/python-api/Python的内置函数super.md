---
title: Python的内置函数super
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 super](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.super.md)

Python 的内置函数 super() 是一个非常重要的内置函数，主要用于在子类中调用父类（超类）的方法。这个函数在面向对象编程中扮演着关键角色，特别是在处理继承关系时。

#### 基本用法

super() 最常见的用法是在子类的初始化方法中调用父类的初始化方法：

```python
class Parent:
    def __init__(self, name):
        self.name = name

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)  # 调用父类的__init__方法
        self.age = age

```

#### 工作原理

1. **方法解析顺序（MRO）**：super() 遵循 Python 的方法解析顺序（Method Resolution Order），这个顺序可以通过 `ClassName.__mro__` 查看
2. **动态绑定**：super() 返回的是一个代理对象，它会根据当前的方法解析顺序来查找方法
3. **两种调用形式**：  
   * Python 3 中可以直接使用 [`super()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.super.md)  
   * Python 2 中需要显式传入类名和实例：[`super(Child, self)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.super.md)

#### 高级用法

1. **多重继承**：在多重继承的情况下，super() 可以确保所有父类的方法都被正确调用

```python
class A:
    def method(self):
        print("A method")

class B(A):
    def method(self):
        print("B method")
        super().method()

class C(A):
    def method(self):
        print("C method")
        super().method()

class D(B, C):
    def method(self):
        print("D method")
        super().method()

d = D()
d.method()  # 输出顺序：D -> B -> C -> A

```

1. **类方法中的使用**：

```python
class Parent:
    @classmethod
    def create(cls):
        return cls()

class Child(Parent):
    @classmethod
    def create(cls):
        obj = super().create()
        obj.extra = "value"
        return obj

```

#### 注意事项

1. **Python 2 和 3 的区别**：Python 2 中必须显式传递参数，Python 3 可以省略
2. **单继承和多继承**：在单继承中，super() 的行为直观；在多继承中，需要理解 MRO 才能正确使用
3. **不要滥用**：只有在确实需要调用父类方法时才使用 super()

#### 典型应用场景

1. 初始化父类状态
2. 扩展父类方法
3. 实现协作式多重继承
4. 代理模式实现

super() 是 Python 实现面向对象编程中方法重载和扩展的重要机制，正确理解和使用它可以帮助开发者编写更清晰、更易维护的代码。

---

> 《[Python 的内置函数 super](https://xplanc.online/68f713a0008737d4b723915535286f4ae1b461d24020c632c8131a8c71c7f47d)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/151939273)。