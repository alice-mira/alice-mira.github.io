---
title: Python的内置函数oct
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 oct](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md)

Python 的内置函数 [`oct()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md) 用于将一个整数转换为八进制（以 8 为基数）字符串表示形式。该函数返回的字符串以 `0o` 为前缀，表示这是一个八进制数。

#### 语法

```python
oct(x)

```

#### 参数

* `x`：必须是一个整数（可以是十进制、二进制、十六进制或其他形式的整数）。如果 `x` 不是整数，则需要先实现 `__index__()` 方法返回一个整数。

#### 返回值

返回一个以 `0o` 为前缀的八进制字符串。

#### 示例

1. **十进制转八进制**  
```python  
print(oct(10))  # 输出：0o12  
```  
解释：十进制 `10` 对应的八进制是 `12`（1×8 + 2×1 = 10）。
2. **二进制转八进制**  
```python  
print(oct(0b1010))  # 输出：0o12  
```  
解释：二进制 `0b1010` 对应的十进制是 `10`，转换为八进制是 `12`。
3. **十六进制转八进制**  
```python  
print(oct(0xA))  # 输出：0o12  
```  
解释：十六进制 `0xA` 对应的十进制是 `10`，转换为八进制是 `12`。
4. **负数转换**  
```python  
print(oct(-10))  # 输出：-0o12  
```  
解释：负数会被转换为带负号的八进制字符串。
5. **非整数对象（需实现 `__index__` 方法）**  
```python  
class MyNumber:  
    def __index__(self):  
        return 10  
num = MyNumber()  
print(oct(num))  # 输出：0o12  
```  
解释：自定义对象需实现 `__index__()` 方法才能使用 [`oct()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md) 函数。

#### 注意事项

* [`oct()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md) 只能用于整数类型的数据。如果传入浮点数或其他类型的数据，会抛出 `TypeError`。
* 返回的字符串包含 `0o` 前缀，这是 Python 中表示八进制的标准方式。

#### 应用场景

1. **系统权限设置**：在 Unix/Linux 系统中，文件权限通常用八进制表示（如 `0o755` 表示 `rwxr-xr-x`）。
2. **嵌入式开发**：某些硬件寄存器的配置可能需要八进制数值。
3. **数据转换**：在需要将数值转换为不同进制表示的场合（如进制转换工具或教学演示）。

通过 [`oct()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md) 函数，可以方便地将整数转换为八进制字符串，便于特定场景下的使用和展示。

---

> 《[Python 的内置函数 oct](https://xplanc.online/d36ca0798221f19707f23ddfe0de5ecc92e1a0494aef557413d38e955b658664)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149032904)。