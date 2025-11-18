---
title: Python的内置函数round
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 round](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.round.md)

Python 的内置函数 [`round()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.round.md) 用于对数字进行四舍五入操作。它的基本语法如下：

```python
round(number, ndigits)

```

其中：

* `number` 是需要进行四舍五入的数字
* `ndigits` 是保留的小数位数（可选参数）

详细说明：

1. 当省略 `ndigits` 参数时，函数会返回最接近的整数
2. `ndigits` 可以为负数，表示对整数部分进行四舍五入（例如十位、百位等）

应用示例：

```python
# 基本用法
print(round(3.14159))      # 输出：3
print(round(3.14159, 2))   # 输出：3.14

```

注意事项：

1. 浮点数精度问题可能导致看似意外的结果
2. 如果 `ndigits` 为负数，`number` 必须是整数或浮点数
3. 在金融计算等对精度要求高的场景，建议使用 decimal 模块而非 round()

与其它语言的差异：

1. Python 2 的四舍五入规则与 Python 3 不同
2. 某些语言（如C语言）采用四舍五入到远离零的方向

---

> 《[Python 的内置函数 round](https://xplanc.online/f5dae714b77ff9f0aaef7ea5595839eb10d2a2925672522559b3f004b9e989c2)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149138013)。