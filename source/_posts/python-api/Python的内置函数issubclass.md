---
title: Python的内置函数issubclass
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 issubclass](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.issubclass.md)

Python 的内置函数 [`issubclass`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.issubclass.md) 用于检查一个类是否是另一个类的子类（直接或间接继承）。它是 Python 面向对象编程中类型检查的重要工具。

#### 语法

```python
issubclass(class, classinfo)

```

#### 参数说明

* `class`：需要检查的类（必须是类对象，不能是实例）
* `classinfo`：可以是一个类对象，或者由类对象组成的元组

#### 返回值

返回布尔值：

* `True`：如果 `class` 是 `classinfo` 的子类
* `False`：其他情况

#### 工作方式

1. 当 `classinfo` 是单个类时，检查标准的继承关系
2. 当 `classinfo` 是元组时，检查 `class` 是否是其中任何一个类的子类
3. 会自动处理多重继承的情况

#### [示例代码](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBBbmltYWwlM0ElMEElMjAlMjAlMjAlMjBwYXNzJTBBJTBBY2xhc3MlMjBNYW1tYWwoQW5pbWFsKSUzQSUwQSUyMCUyMCUyMCUyMHBhc3MlMEElMEFjbGFzcyUyMERvZyhNYW1tYWwpJTNBJTBBJTIwJTIwJTIwJTIwcGFzcyUwQSUwQSUyMyUyMCVFNyVBRSU4MCVFNSU4RCU5NSVFNyVCQiVBNyVFNiU4OSVCRiVFNiVBMyU4MCVFNiU5RiVBNSUwQXByaW50KGlzc3ViY2xhc3MoRG9nJTJDJTIwTWFtbWFsKSklMjAlMjAlMjMlMjBUcnVlJTBBcHJpbnQoaXNzdWJjbGFzcyhEb2clMkMlMjBBbmltYWwpKSUyMCUyMCUyMyUyMFRydWUlMjAoJUU5JTk3JUI0JUU2JThFJUE1JUU3JUJCJUE3JUU2JTg5JUJGKSUwQXByaW50KGlzc3ViY2xhc3MoRG9nJTJDJTIwRG9nKSklMjAlMjAlMjAlMjAlMjAlMjMlMjBUcnVlJTIwKCVFNyU5QiVCOCVFNSU5MCU4QyVFNyVCMSVCQiklMEElMEElMjMlMjAlRTQlQkQlQkYlRTclOTQlQTglRTUlODUlODMlRTclQkIlODQlRTYlQTMlODAlRTYlOUYlQTUlMEFwcmludChpc3N1YmNsYXNzKERvZyUyQyUyMChzdHIlMkMlMjBNYW1tYWwpKSklMjAlMjAlMjMlMjBUcnVlJTBBJTBBJTIzJTIwJUU5JTlEJTlFJUU3JUJCJUE3JUU2JTg5JUJGJUU1JTg1JUIzJUU3JUIzJUJCJTBBcHJpbnQoaXNzdWJjbGFzcyhEb2clMkMlMjBzdHIpKSUyMCUyMCUyMCUyMCUyMCUyMyUyMEZhbHNl)

```python
class Animal:
    pass

class Mammal(Animal):
    pass

class Dog(Mammal):
    pass

# 简单继承检查
print(issubclass(Dog, Mammal))  # True
print(issubclass(Dog, Animal))  # True 

# 使用元组检查
print(issubclass(Dog, (str, Mammal)))  # True

# 非继承关系
print(issubclass(Dog, str))     # False

```

#### 注意事项

1. 第一个参数必须是类对象，不能是实例  
```python  
d = Dog()  
# issubclass(d, Mammal)  # 会引发 TypeError  
```
2. 如果 `classinfo` 不是类或元组，会引发 TypeError
3. 虚基类（通过 ABC 模块创建的抽象基类）也能被正确识别

#### 典型应用场景

1. 类型检查与验证
2. 框架开发中的插件系统
3. 接口实现验证
4. 动态类注册系统

#### 与 isinstance() 的区别

* [`isinstance()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md) 检查对象实例与类的关系
* [`issubclass()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.issubclass.md) 检查类与类之间的关系

在 Python 3 中，[`issubclass`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.issubclass.md) 还支持检查协议类（Protocol classes）和抽象基类（ABCs），使其在现代 Python 类型系统中更加灵活。

---

> 《[Python 的内置函数 issubclass](https://xplanc.online/076107e0bf1965b12dbe004e5c533fa5162591ee6e99def7e6982e4cf79db288)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148883032)。