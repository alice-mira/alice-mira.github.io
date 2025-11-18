---
title: Python的内置函数ord
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 ord](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.ord.md)

Python 的内置函数 [`ord()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.ord.md) 是一个非常有用的字符串处理函数，它主要用于获取单个字符的 Unicode 码点值。具体来说，[`ord()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.ord.md) 函数接受一个长度为 1 的字符串（即单个字符）作为参数，并返回该字符对应的 Unicode 码点的整数数值。

语法格式：

```python
ord(c)

```

其中 `c` 是一个表示单个字符的字符串。

主要特点：

1. 只能处理单个字符，如果传入字符串长度超过1会抛出 TypeError
2. 对 ASCII 字符返回其 ASCII 值
3. 返回值是一个整数

常见应用场景：

1. 字符编码转换和字符处理
2. 实现简单的加密算法
3. 开发字符相关算法（如字符排序、字符统计等）
4. 处理特殊符号或非ASCII字符

示例用法：

```python
print(ord('A'))    # 输出：65（ASCII码）
print(ord('中'))   # 输出：20013（汉字"中"的Unicode码点）

```

注意事项：

1. 对应的逆操作是 [`chr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.chr.md) 函数，可以将 Unicode 码点转换为字符
2. 在 Python 2 中，[`ord()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.ord.md) 也可以用于字节对象（bytes），但在 Python 3 中只能用于字符串
3. 对于空字符串或多字符字符串会抛出 TypeError 异常

---

> 《[Python 的内置函数 ord](https://xplanc.online/82d2c97099c4cf3260006b349485f7a08e930c13743885692193ceb7076363d6)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149035589)。