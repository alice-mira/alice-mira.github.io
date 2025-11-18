---
title: Python的内置函数str
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 str](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md)

Python 的内置函数 [`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 是一个非常重要的类型转换函数，用于将其他数据类型转换为字符串类型。它在 Python 编程中有广泛的应用场景，下面详细介绍其功能和用法：

#### 基本功能

[`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 函数的主要作用是将给定的对象转换为字符串表示形式。当调用 [`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 时，它会尝试调用对象的 `__str__()` 方法（如果存在）来获取其字符串表示。

#### 语法格式

```python
str(object='', encoding='utf-8', errors='strict')

```

* [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)：要转换为字符串的对象（可选参数，默认为空字符串）
* `encoding`：指定编码方式（仅当对象是 bytes 或 bytearray 时需要）
* `errors`：指定编码错误的处理方式

#### 转换示例

1. **数字转字符串**

```python
num = 123
str_num = str(num)  # 结果为 "123"

```

1. **布尔值转字符串**

```python
bool_val = True
str_bool = str(bool_val)  # 结果为 "True"

```

1. **列表转字符串**

```python
list_data = [1, 2, 3]
str_list = str(list_data)  # 结果为 "[1, 2, 3]"

```

1. **自定义对象转字符串**

```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def __str__(self):
        return f"Person: {self.name}"

p = Person("Alice")
str_person = str(p)  # 结果为 "Person: Alice"

```

#### 编码转换

[`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 还可以用于字节序列到字符串的转换：

```python
byte_data = b'Python'
str_data = str(byte_data, encoding='utf-8')  # 结果为 "Python"

```

#### 注意事项

1. 如果对象没有定义 `__str__()` 方法，会回退到 `__repr__()` 方法
2. 转换浮点数时会有精度损失：

```python
pi = 3.141592653589793
str_pi = str(pi)  # 结果为 "3.141592653589793"

```

#### 实际应用场景

1. **日志记录**：将各种数据类型统一转换为字符串进行记录
2. **用户界面显示**：将数据转换为可读的字符串形式
3. **文件操作**：将非字符串数据转换为字符串后写入文件
4. **网络通信**：在发送数据前将对象序列化为字符串

[`str()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md) 函数是 Python 中最基础也最常用的类型转换工具之一，掌握它的使用对于编写 Python 程序至关重要。

---

> 《[Python 的内置函数 str](https://xplanc.online/5d2e62132203d51895b3dcdb758fccff9781acda06ebb5cab0729527967288fe)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/150134670)。