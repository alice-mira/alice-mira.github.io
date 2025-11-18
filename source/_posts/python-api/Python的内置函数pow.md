---
title: Python的内置函数ord
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 pow](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.pow.md)

Python 的内置函数 [`pow()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.pow.md) 是一个用于计算幂运算的强大工具。它有两种基本用法，可以计算数值的幂次方，也支持进行模运算。

#### 基本语法

```python
pow(base, exp)

```

#### 参数说明

1. **base**：底数，可以是整数或浮点数
2. **exp**：指数，可以是整数或浮点数

#### 使用示例

1. 基本幂运算：  
```python  
pow(2, 3)    # 返回8 (2的3次方)  
pow(2.5, 2)  # 返回6.25 (2.5的平方)  
```
2. 带模运算：  
```python  
pow(2, 3, 5)  # 返回3 (2^3=8，8%5=3)  
```
3. 负指数运算：  
```python  
pow(2, -3)    # 返回0.125 (1/(2^3))  
```

#### 注意事项

1. 当所有参数为整数时，结果也为整数
2. 当存在浮点数参数时，结果为浮点数
3. 带模运算时，所有参数必须为整数
4. 与 `**` 运算符相比，[`pow()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.pow.md) 在处理大整数时更高效

#### 实际应用场景

1. 密码学算法（如RSA）中的模幂运算
2. 科学计算中的指数运算
3. 金融领域的复利计算

#### 性能考虑

对于大整数运算，[`pow()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.pow.md) 的三参数形式比先计算幂再求模要高效得多，因为它使用了优化算法来避免中间结果的过度膨胀。

#### 与运算符的对比

```python
# 等效于
pow(2, 3) == 2 ** 3
pow(2, 3, 5) == (2 ** 3) % 5

```

---

> 《[Python 的内置函数 pow](https://xplanc.online/bf89d9f737959e4fb4fd882a562d71bbbdbc076d01a6443c16cbfb7512da06e4)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149079053)。