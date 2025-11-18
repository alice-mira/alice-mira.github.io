---
title: Python的内置函数vars
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 vars](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md)

Python 的内置函数 [`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 是一个非常有用的工具函数，主要用于返回对象的 `__dict__` 属性。它可以应用于模块、类、实例以及其他具有 `__dict__` 属性的对象。以下是关于 [`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 函数的详细说明：

#### 基本用法

1. **不带参数调用**：  
 当 [`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 不带参数调用时，它等同于 [`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 函数，返回当前局部作用域的符号表（通常是当前函数的局部变量）。  
```python  
def example():  
    x = 10  
    y = 20  
    print(vars())  # 输出 {'x': 10, 'y': 20}  
example()  
```
2. **带参数调用**：  
 当使用参数调用时，[`vars(obj)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 会返回对象 `obj` 的 `__dict__` 属性，该属性通常是一个字典，存储了对象的属性和值。  
```python  
class MyClass:  
    def __init__(self):  
        self.a = 1  
        self.b = 2  
obj = MyClass()  
print(vars(obj))  # 输出 {'a': 1, 'b': 2}  
```

#### 适用对象

* **模块**：[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 可以返回模块的全局变量字典。  
```python  
import math  
print(vars(math))  # 输出 math 模块的所有属性和函数  
```
* **类和实例**：对于类和实例，[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 返回其 `__dict__` 属性。  
```python  
class Example:  
    class_attr = "class value"  
    def __init__(self):  
        self.instance_attr = "instance value"  
print(vars(Example))  # 输出类的命名空间，包括 class_attr  
obj = Example()  
print(vars(obj))      # 输出实例的命名空间，如 instance_attr  
```
* **其他对象**：如果对象没有 `__dict__` 属性，[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 会抛出 `TypeError` 异常。  
```python  
print(vars(10))  # TypeError: vars() argument must have __dict__ attribute  
```

#### 注意事项

1. **`__dict__` 可变性**：由于 [`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 返回的是对象的 `__dict__`，因此对返回的字典进行修改会影响原对象。  
```python  
obj = MyClass()  
d = vars(obj)  
d['c'] = 3  # 这会动态添加一个新属性到 obj  
print(obj.c)  # 输出 3  
```
2. **与 [`dir()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dir.md) 的区别**：[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 返回的是对象的属性和值，而 [`dir()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dir.md) 返回的是对象的所有属性和方法名称列表（包括继承的）。
3. **动态属性管理**：[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 常用于动态检查或修改对象的属性，特别是在元编程或调试时。

#### 应用场景

* **调试**：快速检查对象的属性和值。
* **动态编程**：运行时动态添加或修改对象属性。
* **序列化**：获取对象的状态字典以便序列化存储。

[`vars()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.vars.md) 是一个强大但需要谨慎使用的工具，合理使用可以简化代码，但过度依赖可能会降低代码的可读性和可维护性。

---

> 《[Python 的内置函数 vars](https://xplanc.online/3e5aae72080a8428f92260125a428bfd28ed3c21f8c2c1962a7b0eb6a1b494ea)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/152422016)。