---
title: Python的内置函数open
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 open](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.open.md)

Python 的内置函数 [`open()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.open.md) 是用于打开文件的重要函数，它提供了与文件系统交互的基本接口。该函数返回一个文件对象（file object），可用于读取、写入或追加文件内容。

#### 函数签名

```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)

```

#### 主要参数说明

1. **file**（必需）：文件路径（字符串或字节对象），可以是绝对路径或相对路径
2. **mode**（可选）：文件打开模式，默认是 ‘r’（只读）  
   * ‘r’：读取模式（默认）  
   * ‘w’：写入模式，会覆盖已有文件  
   * ‘x’：独占创建模式，文件已存在则报错  
   * ‘a’：追加模式  
   * ‘b’：二进制模式  
   * ‘t’：文本模式（默认）  
   * ‘+’：更新模式（可读写）
3. **encoding**（重要）：指定文本编码格式，如 ‘utf-8’（Python 3默认）、‘gbk’ 等

#### 典型使用示例

1. 读取文本文件：

```python
with open('example.txt', 'r', encoding='utf-8') as f:
    content = f.read()

```

1. 写入文件：

```python
with open('output.txt', 'w') as f:
    f.write('Hello, World!')

```

1. 追加内容：

```python
with open('log.txt', 'a') as f:
    f.write('New log entry\n')

```

1. 二进制文件操作：

```python
with open('image.jpg', 'rb') as f:
    data = f.read()

```

#### 最佳实践建议

1. 始终使用 `with` 语句，确保文件正确关闭
2. 明确指定编码格式，避免跨平台问题
3. 处理大文件时考虑逐行读取或分块读取
4. 注意不同操作系统路径分隔符的差异
5. 检查文件是否存在（os.path.exists）后再操作

#### 常见问题

* 文件不存在时会抛出 FileNotFoundError（读取模式）
* 编码错误会抛出 UnicodeDecodeError
* 权限不足会抛出 PermissionError
* Windows 系统路径需要使用原始字符串或双反斜杠

#### 性能考虑

* 缓冲区大小（buffering）影响 I/O 性能
* 二进制模式比文本模式效率更高
* 大量小文件操作应考虑批量处理

---

> 《[Python 的内置函数 open](https://xplanc.online/7cc07c7aa57ec43f1abbd249b5cc866216f276b6b67e401ec51689572dbac76e)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149035582)。