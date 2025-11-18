---
title: Python的内置函数staticmethod
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 staticmethod](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.staticmethod.md)

Python 的内置函数 [`staticmethod`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.staticmethod.md) 用于将一个方法转换为静态方法。静态方法不需要隐式地传递任何参数（如 `self` 或 `cls`），它们与普通函数类似，但属于类的命名空间。

#### 使用方法

1. **定义静态方法**：在类中使用 [`@staticmethod`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.staticmethod.md) 装饰器来定义静态方法。  
```python  
class MyClass:  
    @staticmethod  
    def static_method(arg1, arg2):  
        return arg1 + arg2  
```
2. **调用静态方法**：可以通过类名或实例调用静态方法，无需传递 `self` 或 `cls` 参数。  
```python  
# 通过类名调用  
result = MyClass.static_method(1, 2)  # 输出 3  
```

#### 特性和应用场景

1. **无绑定参数**：静态方法不需要 `self` 或 `cls` 参数，因此它们不能访问或修改类或实例的状态。
2. **逻辑分组**：如果某个方法与类相关，但不需要访问实例或类属性，可以将其定义为静态方法，以保持代码的逻辑分组。
3. **工具函数**：静态方法常用于实现与类相关的工具函数，例如输入验证、辅助计算等。

#### 示例

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

# 调用静态方法
print(MathUtils.add(5, 3))  # 输出 8

```

#### 注意事项

* 静态方法不能访问类属性或实例属性，除非通过类名或实例显式传递。
* 如果方法需要访问类或实例的状态，应使用实例方法或类方法（[`@classmethod`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.classmethod.md)）代替。

---

> 《[Python 的内置函数 staticmethod](https://xplanc.online/c418e93b0300eeb273b163c1c30529ea58124f33171a55cb4765952581e33e19)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149954032)。