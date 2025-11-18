---
title: Python的内置函数ascii
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 ascii](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.hide/EX.ascii.md)

ascii()函数是Python提供的一个小巧但强大的工具，它能够将任何对象转换为只包含ASCII字符的表示形式，非ASCII字符会被转义。这个函数在调试、日志记录、数据序列化等场景中特别有用，尤其是在需要确保输出只包含可打印ASCII字符的环境中。

ascii 的函数原型：

```python
def ascii(obj):
    '''
    转换为字符串（调用对象的 `__repr__` 方法），非 ASCII 字符将被转义

    :param obj: 一个对象
    :return: obj.__repr__ 返回的字符串
    '''

```

### 示例

[在线运行](https://xplanc.org/shift/?lang=python&code=cHJpbnQoYXNjaWkoJTIySGVsbG8lMjAlRTQlQjglOTYlRTclOTUlOEMlMjIpKQ%3D%3D)

```python
print(ascii("Hello 世界"))

```

---

> 《[Python 的内置函数 ascii](https://xplanc.online/df6e09c5ff2cf356bfc3338fd24b4d0cdebfd8551274eb8970d9fa73d65bf748)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148542195)。