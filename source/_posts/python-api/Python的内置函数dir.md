---
title: Python的内置函数dir
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 dir](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dir.md)

Python 的内置函数 [`dir()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dir.md) 是一个非常有用的工具函数，主要用于获取对象的属性和方法列表。该函数在不同使用场景下会返回不同类型的信息：

```python
def dir(obj):
    '''
    返回对象的成员列表

    :param obj: 一个对象
    :return: 对象的成员列表
    '''

```

* **不带参数使用时**会返回当前作用域中的名称列表
* **带参数使用时**会返回指定对象的有效属性列表

典型应用场景包括：

* 对象探索：快速查看一个对象支持的操作
* 调试帮助：检查对象实际拥有的属性和方法
* 动态编程：结合 [`getattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 和 [`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md) 进行动态属性访问
* 交互式学习：在Python shell中探索对象结构

[运行](https://xplanc.org/shift/?lang=python&code=aW1wb3J0JTIwbWF0aCUwQXByaW50KGRpcigpKSUyMCUyMCUyMyUyMCVFNiU5RiVBNSVFNyU5QyU4QiVFNSVCRCU5MyVFNSU4OSU4RCVFNiVBOCVBMSVFNSU5RCU5NyVFNyU5QSU4NCVFNSU5MCU4RCVFNyVBNyVCMCVFNyVBOSVCQSVFOSU5NyVCNCUwQXByaW50KGRpcihtYXRoKSklMjAlMjAlMjMlMjAlRTYlOUYlQTUlRTclOUMlOEJtYXRoJUU2JUE4JUExJUU1JTlEJTk3JUU3JTlBJTg0JUU2JTg5JTgwJUU2JTlDJTg5JUU1JUIxJTlFJUU2JTgwJUE3JUU1JTkyJThDJUU2JTk2JUI5JUU2JUIzJTk1JTBBJTBBY2xhc3MlMjBNeUNsYXNzJTNBJTBBJTIwJTIwJTIwJTIwZGVmJTIwX19pbml0X18oc2VsZiklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLnZhbHVlJTIwJTNEJTIwNDIlMEElMjAlMjAlMjAlMjBkZWYlMjBzaG93KHNlbGYpJTNBJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwcHJpbnQoc2VsZi52YWx1ZSklMEElMEFvYmolMjAlM0QlMjBNeUNsYXNzKCklMEFwcmludChkaXIob2JqKSklMjAlMjAlMjMlMjAlRTYlOUYlQTUlRTclOUMlOEIlRTUlQUUlOUUlRTQlQkUlOEIlRTclOUElODQlRTUlQjElOUUlRTYlODAlQTclRTUlOTIlOEMlRTYlOTYlQjklRTYlQjMlOTU%3D) 示例程序：

```python
import math
print(dir())  # 查看当前模块的名称空间
print(dir(math))  # 查看math模块的所有属性和方法

class MyClass:
    def __init__(self):
        self.value = 42
    def show(self):
        print(self.value)

obj = MyClass()
print(dir(obj))  # 查看实例的属性和方法

```

注意事项：

* 返回的列表是字母顺序排序的
* 可能包含大量内置特殊方法（以双下划线开头和结尾）
* 不是所有列出的属性都适合直接使用，需结合文档

---

> 《[Python 的内置函数 dir](https://xplanc.online/60707f3e3846e7560d8ae5e8608c76cca0a86669598e4eb3feb3ef44f3f5e756)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148662847)。