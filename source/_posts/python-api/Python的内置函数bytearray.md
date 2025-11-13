---
title: Python的内置函数bytearray
tags: [后端,python,API]
date: 2025-10-13 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 bytearray](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md)

```python
class bytearray(x=b''):
    '''
    创建 bytearray

    :param x: 要转换的变量
    :return: x 转换为 bytearray 后的值
    '''

```

Python 的内置函数 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 是一个可变序列，用于存储字节数据。它类似于 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 类型，但主要区别在于 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 是可变的，而 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 是不可变的。以下是关于 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 的详细说明和使用场景：

#### **1\. 基本语法**

```python
bytearray([source[, encoding[, errors]]])

```

* **source**（可选）：可以是整数、字符串、可迭代对象或缓冲区对象。
* **encoding**（可选）：如果 source 是字符串，需要指定编码格式（如 `'utf-8'`）。
* **errors**（可选）：指定编码错误处理方式（如 `'strict'`、`'ignore'`、`'replace'`）。

#### **2\. 创建 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 的方式**

##### **(1) 创建空 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md)**

```python
ba = bytearray()
print(ba)  # 输出：bytearray(b'')

```

##### **(2) 指定长度的 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md)（整数初始化）**

```python
ba = bytearray(5)  # 创建 5 个字节，默认值为 0
print(ba)  # 输出：bytearray(b'\x00\x00\x00\x00\x00')

```

##### **(3) 从字符串转换**

```python
ba = bytearray("hello", "utf-8")
print(ba)  # 输出：bytearray(b'hello')

```

##### **(4) 从迭代对象（如列表）转换**

```python
ba = bytearray([65, 66, 67])  # ASCII 码对应 A, B, C
print(ba)  # 输出：bytearray(b'ABC')

```

##### **(5) 从 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 转换**

```python
b = b"example"
ba = bytearray(b)
print(ba)  # 输出：bytearray(b'example')

```

#### **3\. [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 的特性**

* **可变性**：可以修改其中的字节值。  
```python  
ba = bytearray(b"hello")  
ba[0] = 72  # 修改第一个字节为大写 'H'  
print(ba)  # 输出：bytearray(b'Hello')  
```
* **支持列表操作**：  
   * 可以添加、删除、修改元素。  
   * 支持切片操作。

#### **4\. 常见应用场景**

* **二进制数据处理**：适用于解析或修改二进制文件、网络协议等场景。  
```python  
data = bytearray(b"\x01\x02\x03")  
data.append(4)  # 添加字节 0x04  
```
* **临时缓冲区**：需要动态修改的二进制数据缓冲区。  
```python  
buffer = bytearray()  
buffer.extend(b"data")  
```
* **文本处理（编码转换）**：如从不同编码格式转换字节数据。  
```python  
text = "你好"  
ba = bytearray(text.encode("utf-8"))  
```

#### **5\. 与 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 的区别**

| 特性   | bytearray | bytes      |
| ---- | --------- | ---------- |
| 可变性  | ✅ 可修改     | ❌ 不可修改     |
| 性能   | 稍慢（可变开销）  | 更快（不可变优化）  |
| 适用场景 | 需要动态修改字节  | 固定不变的二进制数据 |

#### **6\. 总结**

[`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 提供了一种灵活的方式处理可变二进制数据，适用于需要动态修改字节的场景，如网络通信、二进制文件操作等。如果数据不需要修改，建议使用 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 以提高性能。

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148572221)。