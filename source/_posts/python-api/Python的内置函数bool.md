---
title: Python的内置函数bool
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 bool](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bool.md)

在编程中，我们经常需要判断某个值是“真”（True）还是“假”（False），而 bool() 函数就是 Python 提供的用于进行布尔值转换的强大工具。无论是数字、字符串、列表，还是自定义对象，bool() 都能帮助我们快速评估它们的真假状态。

[`bool`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bool.md) 是一个类，它的参数如下：

```python
class bool(x=False):
    '''
    类型转换为 bool

    :param x: 一个变量
    :return: 转换为 bool 后的值
    '''

```

以下值会被转换为 `False`：

* None 和 False 自身
* 0， 0.0，Decimal(0)，0j
* 长度为 0 的字符串、列表、元组等

示例：

```python
print("0 是", bool(0))
print("10 是", bool(10))
print("'hello world' 是", bool('hello world'))
print("'' 是", bool(''))
print("None 是", bool(None))

```

[Python 的内置函数 bool 的示例](https://xplanc.org/shift/?lang=python&code=cHJpbnQoJTIyMCUyMCVFNiU5OCVBRiUyMiUyQyUyMGJvb2woMCkpJTBBcHJpbnQoJTIyMTAlMjAlRTYlOTglQUYlMjIlMkMlMjBib29sKDEwKSklMEFwcmludCglMjInaGVsbG8lMjB3b3JsZCclMjAlRTYlOTglQUYlMjIlMkMlMjBib29sKCdoZWxsbyUyMHdvcmxkJykpJTBBcHJpbnQoJTIyJyclMjAlRTYlOTglQUYlMjIlMkMlMjBib29sKCcnKSklMEFwcmludCglMjJOb25lJTIwJUU2JTk4JUFGJTIyJTJDJTIwYm9vbChOb25lKSk%3D)

---

> 《[Python 的内置函数 bool](https://xplanc.online/50788bac056be12d31708843494367c8d58650d9bae1419c5fc32c79b69aeb9a)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148559782)。