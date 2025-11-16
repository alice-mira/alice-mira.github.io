---
title: Python的内置函数int
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 int](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md)

Python 的内置函数 [`int()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 是一个用于将其他数据类型转换为整数类型的重要函数。它具有以下详细特性：

1. 基本功能：  
   * 将数字或字符串转换为整数  
   * 语法：[`int(x, base=10)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md)  
   * 示例：  
   ```python  
   int('123')  # 返回 123  
   int(12.34)  # 返回 12  
   ```
2. 参数说明：  
   * 第一个参数可以是：  
         * 数字（整数或浮点数）  
         * 字符串（仅包含数字字符）  
         * 布尔值（True 转为 1，False 转为 0）  
   * 可选参数 `base` 表示进制（2-36）  
   ```python  
   int('1010', 2)  # 二进制转十进制，返回 10  
   int('A', 16)    # 十六进制转十进制，返回 10  
   ```
3. 特殊行为：  
   * 对浮点数会直接截断小数部分  
   * 字符串处理时会自动忽略前导和尾随空格  
   ```python  
   int('  123  ')  # 返回 123  
   ```  
   * 无效输入会引发 ValueError  
   ```python  
   int('abc')  # 引发 ValueError  
   ```
4. 实际应用场景：  
   * 用户输入处理（将字符串输入转为数值）  
   * 不同进制数转换  
   * 数据清洗和类型转换  
   * 配合 input() 函数使用：  
   ```python  
   age = int(input("请输入年龄："))  
   ```
5. 注意事项：  
   * 无法转换包含非数字字符的字符串  
   * 处理浮点数时是截断而非四舍五入  
   * 大数处理时不会丢失精度（Python 整数无大小限制）

[`int()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 是 Python 数据类型转换的基础函数之一，在数值计算、用户交互和数据预处理中经常使用。Python 的内置函数 int

---

> 《[Python 的内置函数 int](https://xplanc.online/d4a6534ebfd127dfd262bffdd408ca368fe8073efd790b961cd63b0e1a7e0159)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148857705)。