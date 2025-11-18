---
title: Python的内置函数property
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 property](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.property.md)

Python 的内置函数 [`property()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.property.md) 是一个非常重要的工具，用于管理类属性的访问。它提供了一种优雅的方式来定义属性访问器（getter）、设置器（setter）和删除器（deleter）方法，同时保持简洁的接口。

#### 基本用法

```python
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        """获取姓名"""
        return self._name
    
    @name.setter
    def name(self, value):
        if not isinstance(value, str):
            raise ValueError("姓名必须是字符串")
        self._name = value
    
    @name.deleter
    def name(self):
        print("删除姓名")
        del self._name

```

#### 典型应用场景

1. **数据验证**：在设置属性值时进行有效性检查
2. **计算属性**：根据其他属性动态计算值
3. **访问控制**：控制对敏感属性的访问权限
4. **延迟加载**：只在需要时才计算或获取属性值

#### 示例代码

```python
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        """获取姓名"""
        return self._name
    
    @name.setter
    def name(self, value):
        if not isinstance(value, str):
            raise ValueError("姓名必须是字符串")
        self._name = value
    
    @name.deleter
    def name(self):
        print("删除姓名")
        del self._name

```

#### 使用装饰器的优势

使用 [`@property`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.property.md) 装饰器比直接使用 [`property()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.property.md) 函数更为简洁直观。实际上，装饰器语法：

```python
@property
def name(self):
    ...

```

等同于：

```python
name = property(name)

```

#### 注意事项

1. 属性方法应该保持简单，避免复杂的计算或IO操作
2. 不要过度使用 property，对于简单的属性访问直接使用公共属性即可
3. property 不能用于实例方法，只能用于实例属性

#### 进阶用法

property 还可以用于实现：

* 只读属性（只定义 getter）
* 只写属性（只定义 setter）
* 缓存属性（在 getter 中进行缓存）
* 观察者模式（在 setter 中通知观察者）

通过合理使用 property，可以大大提高代码的可维护性和安全性。

---

> 《[Python 的内置函数 property](https://xplanc.online/a7c69d7161077095bfb9c3b82a06068f63341d9fc88b78845e7fe9ea65ca6bac)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149102534)。