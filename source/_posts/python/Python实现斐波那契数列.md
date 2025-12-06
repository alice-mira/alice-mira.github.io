---
title: Python实现斐波那契数列
tags: [后端,python]
date: 2025-12-06 08:08:08
---

# Python实现斐波那契数列

斐波那契数列是一个经典的数学序列，其中每个数字都是前两个数字之和。序列通常以 0 和 1 开始：0, 1, 1, 2, 3, 5, 8, 13, 21, 34,...

## 基本实现方法

### 1. 递归实现
```python
def fibonacci_recursive(n):
    if n <= 1:
        return n
    else:
        return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
```

这种方法简单直观，但效率较低，时间复杂度为 O(2^n)，因为存在大量重复计算。

### 2. 迭代实现
```python
def fibonacci_iterative(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

迭代方法更高效，时间复杂度为 O(n)，空间复杂度为 O(1)。

### 3. 带缓存的递归实现（记忆化）
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci_memoization(n):
    if n <= 1:
        return n
    return fibonacci_memoization(n-1) + fibonacci_memoization(n-2)
```

这种方法结合了递归的简洁性和缓存的高效性，避免了重复计算。

## 进阶实现

### 1. 使用生成器
```python
def fibonacci_generator():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# 使用示例
fib = fibonacci_generator()
first_10 = [next(fib) for _ in range(10)]
```

### 2. 矩阵快速幂方法
```python
def matrix_mult(a, b):
    return [
        [a[0][0]*b[0][0] + a[0][1]*b[1][0], a[0][0]*b[0][1] + a[0][1]*b[1][1]],
        [a[1][0]*b[0][0] + a[1][1]*b[1][0], a[1][0]*b[0][1] + a[1][1]*b[1][1]]
    ]

def matrix_pow(mat, power):
    result = [[1, 0], [0, 1]]  # 单位矩阵
    while power > 0:
        if power % 2 == 1:
            result = matrix_mult(result, mat)
        mat = matrix_mult(mat, mat)
        power //= 2
    return result

def fibonacci_matrix(n):
    if n == 0:
        return 0
    mat = [[1, 1], [1, 0]]
    mat_n = matrix_pow(mat, n-1)
    return mat_n[0][0]
```

这种方法的时间复杂度为 O(log n)，适合计算非常大的斐波那契数。

## 应用场景

1. **算法教学**：常用于演示递归、动态规划等编程概念
2. **金融分析**：用于斐波那契回撤等技术分析
3. **自然界模拟**：描述植物生长、蜂巢结构等自然现象
4. **密码学**：某些加密算法中会用到斐波那契数列

## 性能比较

对于不同实现方法，当 n=35 时的执行时间对比（单位：秒）：

| 方法          | 执行时间 |
|---------------|---------|
| 递归          | ~3.5    |
| 迭代          | ~0.00001|
| 记忆化        | ~0.0001 |
| 矩阵快速幂    | ~0.00005|

当需要计算大数值（如 n>1000）时，矩阵快速幂方法是最高效的选择。