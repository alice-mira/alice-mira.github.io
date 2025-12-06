---
title: Python水仙花数详解
tags: [后端,python]
date: 2025-12-06 13:08:08
---

# Python水仙花数详解

## 什么是水仙花数

水仙花数（Narcissistic number）是指一个n位数，它的每个位上的数字的n次幂之和等于它本身。例如：
- 153是一个3位数的水仙花数，因为1³ + 5³ + 3³ = 1 + 125 + 27 = 153
- 1634是一个4位数的水仙花数，因为1⁴ + 6⁴ + 3⁴ + 4⁴ = 1 + 1296 + 81 + 256 = 1634

水仙花数也被称为自恋数、自幂数或阿姆斯壮数（Armstrong number）。

## Python实现水仙花数判断

### 方法一：基础实现

```python
def is_narcissistic(num):
    # 将数字转换为字符串以获取位数和各位数字
    str_num = str(num)
    n = len(str_num)
    
    # 计算各位数字的n次方之和
    total = sum(int(digit)**n for digit in str_num)
    
    return total == num

# 测试100-10000之间的水仙花数
for i in range(100, 10000):
    if is_narcissistic(i):
        print(i)
```

### 方法二：优化实现（不使用字符串转换）

```python
def is_narcissistic_optimized(num):
    if num < 100:
        return False
    
    original = num
    digits = []
    n = 0
    
    # 分解数字并计算位数
    while num > 0:
        digits.append(num % 10)
        num = num // 10
        n += 1
    
    # 计算各位数字的n次方之和
    total = sum(d**n for d in digits)
    
    return total == original
```

## 常见的水仙花数

以下是已知的水仙花数列表（十进制）：
- 1位数：1, 2, 3, 4, 5, 6, 7, 8, 9
- 3位数：153, 370, 371, 407
- 4位数：1634, 8208, 9474
- 5位数：54748, 92727, 93084
- 6位数：548834
- 7位数：1741725, 4210818, 9800817, 9926315

## 扩展应用

### 寻找指定位数的水仙花数

```python
def find_narcissistic_numbers(digits):
    start = 10**(digits-1)
    end = 10**digits
    results = []
    
    for num in range(start, end):
        if is_narcissistic(num):
            results.append(num)
    
    return results

# 查找所有4位水仙花数
print(find_narcissistic_numbers(4))  # 输出: [1634, 8208, 9474]
```

### 性能优化建议

对于大位数的水仙花数查找，可以考虑以下优化：
1. 预计算数字的幂次结果
2. 使用多线程或多进程并行计算
3. 实现记忆化存储已计算结果

## 数学特性

水仙花数有一些有趣的数学特性：
1. 不存在2位数的水仙花数
2. 水仙花数的数量随着位数的增加而减少
3. 目前已知最大的水仙花数是39位数
4. 水仙花数的总数是有限的（已被证明不超过88个）