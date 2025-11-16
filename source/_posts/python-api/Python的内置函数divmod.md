---
title: Python的内置函数divmod
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 divmod](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.divmod.md)

Python 的内置函数 [`divmod()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.divmod.md) 是一个实用的数学运算函数，它能够同时返回两个数值相除的商和余数。这个函数接受两个非复数数字作为参数，返回一个包含两个元素的元组，第一个元素是两数相除的商，第二个元素是余数。

```python
def divmod(x, y):
    '''
    返回整数除法时的商和余数

    :param x: 被除数
    :param y: 除数
    :return: 商和余数的元组
    '''

```

典型应用场景包括：

1. 时间转换 - 将总秒数转换为小时/分钟/秒格式
2. 进制转换 - 在数字进制转换时同时获取商和余数
3. 分页计算 - 计算总页数和最后一页的项目数

使用示例-时间转换：  
[运行示例](https://xplanc.org/shift/?lang=python&code=dG90YWxfc2Vjb25kcyUyMCUzRCUyMDM2NzAlMEFtaW51dGVzJTJDJTIwc2Vjb25kcyUyMCUzRCUyMGRpdm1vZCh0b3RhbF9zZWNvbmRzJTJDJTIwNjApJTBBaG91cnMlMkMlMjBtaW51dGVzJTIwJTNEJTIwZGl2bW9kKG1pbnV0ZXMlMkMlMjA2MCklMEFwcmludChmJTIyJTdCaG91cnMlN0QlRTUlQjAlOEYlRTYlOTclQjYlN0JtaW51dGVzJTdEJUU1JTg4JTg2JUU5JTkyJTlGJTdCc2Vjb25kcyU3RCVFNyVBNyU5MiUyMiklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUExJUU1JUIwJThGJUU2JTk3JUI2MSVFNSU4OCU4NiVFOSU5MiU5RjEwJUU3JUE3JTky)

```python
total_seconds = 3670
minutes, seconds = divmod(total_seconds, 60)
hours, minutes = divmod(minutes, 60)
print(f"{hours}小时{minutes}分钟{seconds}秒")  # 输出：1小时1分钟10秒

```

与单独使用//和%运算符相比，divmod()的优势在于只需一次计算就能同时获得两个结果，在某些场景下可以提高运算效率。

---

> 《[Python 的内置函数 divmod](https://xplanc.online/658c1918830442f08aebc7be99a991b07165f25255d25f85f282a9c9fa999dd3)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148662900)。