---
title: Python的内置函数type
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 type](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md)

Python 的内置函数 [`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 是一个非常重要的函数，它主要用于获取对象的类型信息。这个函数有两种主要用法：

1. **单参数调用**：  
 当传入一个参数时，[`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 会返回该对象的类型（类）。返回的结果是一个类型对象，通常显示为 `<class '类型名称'>` 的格式。  
示例：  
```python  
print(type(42))         # <class 'int'>  
print(type("hello"))    # <class 'str'>  
print(type([1, 2, 3]))  # <class 'list'>  
print(type(3.14))       # <class 'float'>  
print(type(True))       # <class 'bool'>  
```
2. **三参数调用（用于动态创建类）**：  
[`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 也可以接受三个参数来动态创建新的类：  
   * 第一个参数是新类的名称（字符串）  
   * 第二个参数是基类（元组形式）  
   * 第三个参数是类命名空间（字典形式）  
示例：  
```python  
MyClass = type('MyClass', (), {'x': 10, 'y': 20})  
obj = MyClass()  
print(obj.x)  # 输出: 10  
```

在实际应用中，[`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 常用于：

* 类型检查：在需要验证变量类型时非常有用
* 调试：快速了解变量的类型信息
* 元编程：动态创建类或修改类的行为
* 接口设计：在需要处理多种类型输入时进行类型判断

注意事项：

* 对于类型检查，通常更推荐使用 [`isinstance()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.isinstance.md) 函数，因为它考虑了继承关系
* [`type()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 返回的是对象最直接的类型，不会考虑继承关系
* 在 Python 3 中，所有类都是 [`type`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.type.md) 类的实例

---

> 《[Python 的内置函数 type](https://xplanc.online/ddca4702388569cc06efcf1a2cf4393679d289b0d2e59d8ada0d69b41330857f)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/152260579)。