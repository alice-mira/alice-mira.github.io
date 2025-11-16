---
title: Python的内置函数bytes
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 bytes](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md)

```python
class bytes(x=b''):
    '''
    创建 bytes

    :param x: 要转换的变量
    :return: x 转换为 bytes 后的值
    '''

```

Python 的内置函数 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 用于创建不可变的字节序列对象。它是 Python 中处理二进制数据的基本类型之一，与 [`str`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 类型类似但专门用于表示字节数据而非文本。

[`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 函数有三种主要创建方式：

1. 通过指定长度创建：[`bytes(5)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 会创建一个包含 5 个零字节的序列(b’\\x00\\x00\\x00\\x00\\x00’)
2. 通过可迭代对象创建：[`bytes([65, 66, 67])`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 会创建包含 ASCII 码 65-67 的字节序列(b’ABC’)
3. 通过字符串和编码创建：[`bytes('你好', 'utf-8')`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 会将字符串按指定编码转换为字节序列

字节序列的主要特点包括：

* 不可变性：一旦创建就不能修改
* 取值范围：每个字节必须是 0 <= x < 256 的整数
* 显示方式：可打印字符显示为 ASCII 字符，其他显示为 \\x 加十六进制

常见应用场景：

1. 文件 I/O 操作：[`open('file.bin', 'rb').read()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.open.md) 返回的就是 bytes 对象
2. 网络通信：socket 发送接收的数据通常是 bytes 格式
3. 数据序列化：pickle、json 等模块处理的数据底层都是 bytes
4. 加密算法：哈希、加密等操作通常处理字节数据

与 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 的区别：

1. [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 是不可变的，[`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 是可变的
2. [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 可以直接作为字典键使用，[`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 不行
3. 性能上 [`bytes`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytes.md) 通常比 [`bytearray`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bytearray.md) 稍快

示例用法：

[点击运行](https://xplanc.org/shift/?lang=python&code=JTIzJTIwJUU1JTg4JTlCJUU1JUJCJUJBJTIwYnl0ZXMlMjAlRTUlQUYlQjklRTglQjElQTElMEFiMSUyMCUzRCUyMGJ5dGVzKDMpJTIwJTIwJTIzJTIwYiclNUN4MDAlNUN4MDAlNUN4MDAnJTBBYjIlMjAlM0QlMjBieXRlcyglNUI3MiUyQyUyMDEwMSUyQyUyMDEwOCUyQyUyMDEwOCUyQyUyMDExMSU1RCklMjAlMjAlMjMlMjBiJ0hlbGxvJyUwQWIzJTIwJTNEJTIwYnl0ZXMoJ1B5dGhvbiclMkMlMjAnYXNjaWknKSUyMCUyMCUyMyUyMGInUHl0aG9uJyUwQSUwQSUyMyUyMCVFNSVCOCVCOCVFNyU5NCVBOCVFNiU5NiVCOSVFNiVCMyU5NSUwQWRhdGElMjAlM0QlMjBiJ2V4YW1wbGUnJTBBcHJpbnQoZGF0YS5oZXgoKSklMjAlMjAlMjMlMjAlRTglQkQlQUMlRTYlOEQlQTIlRTQlQjglQkElRTUlOEQlODElRTUlODUlQUQlRTglQkYlOUIlRTUlODglQjYlRTUlQUQlOTclRTclQUMlQTYlRTQlQjglQjIlRUYlQkMlOUEnNjU3ODYxNmQ3MDZjNjUnJTBBcHJpbnQoZGF0YS5kZWNvZGUoJ3V0Zi04JykpJTIwJTIwJTIzJTIwJUU4JUE3JUEzJUU3JUEwJTgxJUU0JUI4JUJBJUU1JUFEJTk3JUU3JUFDJUE2JUU0JUI4JUIyJUVGJUJDJTlBJ2V4YW1wbGUn)

```python
# 创建 bytes 对象
b1 = bytes(3)  # b'\x00\x00\x00'
b2 = bytes([72, 101, 108, 108, 111])  # b'Hello'
b3 = bytes('Python', 'ascii')  # b'Python'

# 常用方法
data = b'example'
print(data.hex())  # 转换为十六进制字符串：'6578616d706c65'
print(data.decode('utf-8'))  # 解码为字符串：'example'

```

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148591643)。