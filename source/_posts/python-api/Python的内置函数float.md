---
title: Python的内置函数float
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 float](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md)

Python 的内置函数 [`float()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md) 是一个用于将数字或字符串转换为浮点数（即带有小数部分的数字）的函数。它是 Python 中处理数值转换的重要工具之一，常用于数据类型转换和数值计算场景。

#### 功能说明

1. **无参数调用**：当不带任何参数调用时，[`float()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md) 会返回 `0.0`  
```python  
print(float())  # 输出: 0.0  
```
2. **数字转换**：  
   * 整数转换为浮点数  
   ```python  
   print(float(5))  # 输出: 5.0  
   ```  
   * 布尔值转换（True→1.0，False→0.0）  
   ```python  
   print(float(True))  # 输出: 1.0  
   ```
3. **字符串转换**：  
   * 可以处理十进制字符串  
   ```python  
   print(float("3.14"))  # 输出: 3.14  
   ```  
   * 支持科学计数法表示  
   ```python  
   print(float("1e-3"))  # 输出: 0.001  
   ```
4. **特殊值处理**：  
   * 可以识别字符串形式的特殊值  
   ```python  
   print(float("inf"))  # 输出: inf（正无穷）  
   print(float("-inf"))  # 输出: -inf（负无穷）  
   print(float("nan"))  # 输出: nan（非数字）  
   ```

#### 使用注意事项

1. **错误处理**：  
```python  
try:  
    float("python")  # 会引发 ValueError  
except ValueError as e:  
    print(f"转换失败: {e}")  
```
2. **与 int()的区别**：  
   * [`float()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md) 保留小数部分  
   * [`int()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 会截断小数部分
3. **精度问题**：  
   * 浮点数运算可能存在精度问题  
   * 示例：  
   ```python  
   print(0.1 + 0.2)  # 输出: 0.30000000000000004  
   ```

#### 实际应用场景

1. **用户输入处理**：  
```python  
user_input = input("请输入一个数字: ")  
try:  
    number = float(user_input)  
    print(f"你输入的数字是: {number}")  
except ValueError:  
    print("请输入有效的数字")  
```
2. **数据清洗**：  
```python  
data = ["1.5", "2", "3.14", "invalid"]  
cleaned = []  
for item in data:  
    try:  
        cleaned.append(float(item))  
    except ValueError:  
        pass  
print(cleaned)  # 输出: [1.5, 2.0, 3.14]  
```
3. **科学计算**：  
```python  
# 计算圆的面积  
radius = float(input("请输入半径: "))  
area = 3.1415926 * radius ** 2  
print(f"圆的面积是: {area}")  
```

[`float()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md) 函数是 Python 数值处理的基础工具，掌握它的使用对于进行数值计算和数据处理非常重要。在使用时要注意异常处理和浮点数精度问题，特别是在需要高精度计算的场合可能需要使用 `decimal` 模块替代。

---

> 《[Python 的内置函数 float](https://xplanc.online/9462ce229af71fd10048b2ca7605d90557691ca4899b4e1fdb77f916e23d15c0)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148728245)。