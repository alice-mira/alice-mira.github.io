---
title: Python的内置函数reversed
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 reversed](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md)

Python 的内置函数 [`reversed()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) 是一个用于序列反转的高效工具函数，它返回一个反向迭代器对象。以下是关于该函数的详细说明：

1. 基本用法
* 语法：[`reversed(seq)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md)
* 参数：`seq` 可以是任何实现了 `__reversed__()` 方法的对象，或者支持序列协议(`__len__()` 和 `__getitem__()` 方法)的对象
* 返回值：返回一个反向迭代器对象
1. 支持的数据类型
* 列表：[`reversed([1, 2, 3])`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) → 返回 `[3, 2, 1]` 的迭代器
* 元组：[`reversed((1, 2, 3))`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) → 返回 `(3, 2, 1)` 的迭代器
* 字符串：[`reversed("abc")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) → 返回 `"cba"` 的迭代器
* 范围对象：[`reversed(range(5))`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) → 返回 `4, 3, 2, 1, 0` 的迭代器
1. 实际应用示例

```python
# 反转列表
lst = [1, 2, 3, 4]
for num in reversed(lst):
    print(num)  # 输出：4, 3, 2, 1

# 字符串反转
s = "hello"
reversed_str = ''.join(reversed(s))  # "olleh"

# 自定义类的反转
class MySeq:
    def __init__(self, data):
        self.data = data
    
    def __len__(self):
        return len(self.data)
    
    def __getitem__(self, index):
        return self.data[index]

seq = MySeq([10, 20, 30])
for item in reversed(seq):
    print(item)  # 输出：30, 20, 10

```

1. 性能特点
* [`reversed()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) 不会创建新的序列，而是返回一个迭代器，因此内存效率高
* 与切片反转 `seq[::-1]` 相比，[`reversed()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md) 更节省内存，特别是处理大型序列时
* 时间复杂度为 O(1)，因为它只是返回一个反向访问的迭代器
1. 注意事项
* 返回的迭代器是一次性的，再次迭代需要重新调用 [`reversed()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.reversed.md)
* 对于不可变序列(如字符串)，需要配合 `join()` 等方法才能得到反转后的结果
* 不支持直接反转字典和集合，因为它们是无序的数据结构

---

> 《[Python 的内置函数 reversed](https://xplanc.online/198121e975ee2800fdad0ea154dfd16cedfd2bf155ae62d0d5f93a1415bc30ca)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149125827)。