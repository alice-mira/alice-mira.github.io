---
title: Python3的变化
tags: [后端,python]
---

[官方文档](https://docs.python.org/3/)

[python教程](https://docs.python.org/3/tutorial/)

window系统下查看python版本

win+R键打开cmd输入下面的命令

```txt
python --version

```

或者

```txt
python -V

```

类似c语言以.c为后缀，c++以.cpp为后缀，python文件的扩展名以.py结尾

> Jupyter Notebook文件以.ipynb为后缀,该类文件通常包含代码、文本和可视化结果

## Python 3简介

Python 3 是一种高级、解释型的编程语言，广泛用于 Web 开发、数据科学、机器学习、自动化、人工智能等领域。与 Python 2 相比，Python 3 在语法、库和功能上进行了改进和更新，旨在提升语言的易用性和一致性。  

#### 文章目录

* [Python 3简介](#Python%5F3%5F22)
* * * [Python 3 的特点](#Python%5F3%5F%5F26)  
         * * [1\. 简洁易读的语法](#1%5F%5F28)  
                  * [2\. Unicode 支持](#2%5FUnicode%5F%5F32)  
                  * [3\. 改进的整数除法](#3%5F%5F36)  
                  * [4\. \[`print\`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 函数](#4%5Fprint%5F%5F40)  
                  * [5\. 改进的标准库](#5%5F%5F50)  
                  * [6\. 更严格的错误处理](#6%5F%5F54)  
                  * [7\. 迭代器与生成器](#7%5F%5F58)  
                  * [8\. 类型注解](#8%5F%5F65)  
                  * [9\. \`async\` 与 \`await\`](#9%5Fasync%5F%5Fawait%5F74)  
                  * [10\. 更高效的内存管理](#10%5F%5F78)  
         * [Python 3 与 Python 2 的差异](#Python%5F3%5F%5FPython%5F2%5F%5F82)  
         * [主要版本](#%5F91)

#### Python 3 的特点

##### 1\. 简洁易读的语法

Python 3 保持了 Python 的核心设计原则：简洁、可读和优雅。它的语法较为直观，代码风格一致，因此非常适合初学者和开发人员。

##### 2\. Unicode 支持

Python 3 完全支持 Unicode，可以处理所有语言的字符集，而 Python 2 默认使用 ASCII 编码。这使得 Python 3 在全球化应用中更为强大，尤其在处理多语言文本时。

##### 3\. 改进的整数除法

在 Python 3 中，整数除法 `3 / 2` 会得到浮动结果 `1.5`，而不是 `1`。如果需要整数除法，使用 `//` 操作符。这样消除了 Python 2 中整数除法的潜在误解。

##### 4\. [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 函数

Python 3 强制 [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 作为一个函数调用，而不是 Python 2 中的语句形式。你需要使用括号，例如：

```txt
print("Hello, World!")

```

这使得 [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 在 Python 3 中更一致，并且可以被当作函数传递。

##### 5\. 改进的标准库

Python 3 的标准库经过重构，许多 Python 2 中的过时模块被淘汰或更新。例如，`urllib` 模块在 Python 3 中被重新设计，简化了 URL 操作。

##### 6\. 更严格的错误处理

Python 3 提供了更一致的异常处理机制。它要求 `except` 语句明确指定异常类型，避免了 Python 2 中有时容易忽略的错误。

##### 7\. 迭代器与生成器

Python 3 中，大多数内置容器（如 [`range`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)、[`map`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.map.md)、[`filter`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.filter.md) 等）返回迭代器而不是列表。这样可以节省内存，尤其在处理大量数据时，性能更优。

* 在 Python 2 中，[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md) 会返回一个完整的列表。
* 在 Python 3 中，[`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md) 返回一个迭代器。

##### 8\. 类型注解

Python 3 引入了类型注解（PEP 484），允许开发者为函数的参数和返回值提供类型提示。虽然 Python 仍然是动态类型语言，但类型注解有助于提高代码的可读性和可维护性，并且可以与静态分析工具（如 `mypy`）配合使用。

```txt
def greet(name: str) -> str:
    return "Hello, " + name

```

##### 9\. `async` 与 `await`

Python 3.5 引入了 `async` 和 `await` 关键字，使得编写异步代码变得更加简单和直观。异步编程使得 Python 更适合用于高并发的应用，如 Web 服务和爬虫。

##### 10\. 更高效的内存管理

Python 3 在内存管理方面进行了优化，尤其是在字符串和容器的实现上。例如，Python 3 对 [`dict`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md)（字典）和 [`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md)（集合）做了优化，增加了更好的性能和内存效率。

#### Python 3 与 Python 2 的差异

虽然 Python 3 在性能、语法和库支持上有显著改进，但由于 Python 2 曾经是主流版本，许多老旧项目仍然在使用 Python 2。因此，Python 3 和 Python 2 存在一些不兼容的地方。主要差异包括：

* **字符串处理**：Python 3 默认使用 Unicode 字符串，而 Python 2 默认为 ASCII。
* **[`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)**：Python 2 中是语句，Python 3 中是函数。
* **除法运算**：Python 2 中整数除法会舍弃小数部分，Python 3 中返回浮点数。
* **`xrange()`**：Python 2 中有 `xrange()`，用于生成数字的迭代器；Python 3 中只有 [`range()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.range.md)，并且返回迭代器。

#### 主要版本

* **Python 3.0**：于 2008 年发布，标志着 Python 2 到 Python 3 的过渡。
* **Python 3.5**：引入了 `async`/`await`。
* **Python 3.6**：引入了 f-string 格式化字符串，增加了语法的简洁性。
* **Python 3.7**：引入了数据类（`dataclasses`），简化了类的定义。
* **Python 3.8**：引入了运算符“海象运算符”（`:=`）等新特性。
* **Python 3.9**：引入了类型注解和一些其他增强功能。
* **Python 3.10**：引入了模式匹配，进一步提升了 Python 的表达能力。

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/qq_64736204/article/details/152846124)。