---
title: Python的内置函数abs
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 abs](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.abs.md)

无论是在数学计算、数据分析，还是日常编程中，我们经常需要获取一个数的绝对值。Python 提供的 abs() 函数，可以让我们轻松地计算数字的绝对值，而无需手动判断正负。

abs 函数的参数和返回值如下：

```python
def abs(x):
    '''
    计算参数的绝对值

    :param x: 要计算的值
    :return: x 的绝对值
    '''

```

### 示例

[在线运行](https://xplanc.org/shift/#lang=python&code=JTIzJTIwKiolRTglQUYlQjQlRTYlOTglOEUqKiUwQSUyMyUyMGFicygpJTIwJUU1JTg3JUJEJUU2JTk1JUIwJUU4JUJGJTk0JUU1JTlCJTlFJUU2JTk1JUIwJUU1JUFEJTk3JUU3JTlBJTg0JUU3JUJCJTlEJUU1JUFGJUI5JUU1JTgwJUJDJUUzJTgwJTgyJTBBJTIzJTIwKiolRTUlOEYlODIlRTYlOTUlQjAqKiUwQSUyMyUyMColMjAlNjB4JTYwJTIwLSUyMCVFOCVBNiU4MSVFOCVBRSVBMSVFNyVBRSU5NyVFNyU5QSU4NCVFNSU4MCVCQyUwQSUyMyUyMCoqJUU4JUJGJTk0JUU1JTlCJTlFJUU1JTgwJUJDKiolMEElMjMlMjAlNjB4JTYwJTIwJUU3JTlBJTg0JUU3JUJCJTlEJUU1JUFGJUI5JUU1JTgwJUJDJTBBJTBBcHJpbnQoYWJzKC0xMDApKSUwQXByaW50KGFicygtMjMzLjMzMzMpKSUwQXByaW50KGFicygwKSklMEFwcmludChhYnMoMTI4KSk%3D)

```python
print(abs(-50))
print(abs(-3.3333))
print(abs(0))
print(abs(26))

```

abs() 虽然简单，但在数学计算、数据清洗、科学计算等领域非常实用。希望你现在能更熟练地使用它，并在实际编程中灵活应用！

---

> 《[Python 的内置函数 abs](https://xplanc.online/a8e2424b3eb4727f51076370e87e800a9580efa841dc24b335f527218f4e8fda)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148495159)。