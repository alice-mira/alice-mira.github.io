---
title: Python的内置函数delattr
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 delattr](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.delattr.md)

```python
def delattr(obj, name:str):
    '''
    删除指定的属性

    :param obj: 一个对象
    :param name: 要删除的属性的名字
    '''

```

Python 的内置函数 [`delattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.delattr.md) 用于动态删除对象的属性。该函数需要两个参数：第一个参数是目标对象，第二个参数是要删除的属性名称（字符串形式）。

### 示例

[运行](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBQZXJzb24lM0ElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2luaXRfXyhzZWxmJTJDJTIwbmFtZSUyQyUyMGFnZSklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLm5hbWUlMjAlM0QlMjBuYW1lJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwc2VsZi5hZ2UlMjAlM0QlMjBhZ2UlMEElMEFwJTIwJTNEJTIwUGVyc29uKCUyMkFsaWNlJTIyJTJDJTIwMjUpJTBBcHJpbnQocC5uYW1lKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMEFsaWNlJTBBJTBBZGVsYXR0cihwJTJDJTIwJTIybmFtZSUyMiklMjAlMjAlMjMlMjAlRTUlODglQTAlRTklOTklQTQlMjBuYW1lJTIwJUU1JUIxJTlFJUU2JTgwJUE3JTBBcHJpbnQoaGFzYXR0cihwJTJDJTIwJTIybmFtZSUyMikpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJTNBJTIwRmFsc2U%3D)

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 25)
print(p.name)  # 输出: Alice

delattr(p, "name")  # 删除 name 属性
print(hasattr(p, "name"))  # 输出: False

```

---

> 《[Python 的内置函数 delattr](https://xplanc.online/1ec0f60fca1a4484175379c9971fe3ccb96d0fbae3cd85cae0b7f2ae20eeff9f)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148645087)。