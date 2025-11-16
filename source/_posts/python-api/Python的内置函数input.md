---
title: Python的内置函数input
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 input](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md)

Python 的内置函数 [`input()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md) 是一个用于获取用户输入的标准函数，它会暂停程序执行，等待用户在控制台输入内容并按回车键确认。这个函数在交互式程序和需要用户参与的脚本中非常有用。

#### 基本用法

[`input()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md) 函数的基本语法如下：

```python
user_input = input([prompt])

```

其中：

* `prompt` 是一个可选参数，用于显示提示信息，告诉用户需要输入什么内容
* 函数返回用户输入的内容，以字符串形式保存

#### 示例代码

1. 最简单的[使用方式](https://xplanc.org/shift/?lang=python&input=dG9t&code=bmFtZSUyMCUzRCUyMGlucHV0KCUyMiVFOCVBRiVCNyVFOCVCRSU5MyVFNSU4NSVBNSVFNCVCRCVBMCVFNyU5QSU4NCVFNSU5MCU4RCVFNSVBRCU5NyVFRiVCQyU5QSUyMiklMEFwcmludChmJTIyJUU0JUJEJUEwJUU1JUE1JUJEJUVGJUJDJThDJTdCbmFtZSU3RCVFRiVCQyU4MSUyMik%3D)：

```python
name = input("请输入你的名字：")
print(f"你好，{name}！")

```

1. 获取[数字输入](https://xplanc.org/shift/?lang=python&input=MTE%3D&code=YWdlJTIwJTNEJTIwaW5wdXQoJTIyJUU4JUFGJUI3JUU4JUJFJTkzJUU1JTg1JUE1JUU0JUJEJUEwJUU3JTlBJTg0JUU1JUI5JUI0JUU5JUJFJTg0JUVGJUJDJTlBJTIyKSUwQWFnZSUyMCUzRCUyMGludChhZ2UpJTIwJTIwJTIzJTIwJUU1JUIwJTg2JUU1JUFEJTk3JUU3JUFDJUE2JUU0JUI4JUIyJUU4JUJEJUFDJUU2JThEJUEyJUU0JUI4JUJBJUU2JTk1JUI0JUU2JTk1JUIwJTBBcHJpbnQoZiUyMiVFNiU5OCU4RSVFNSVCOSVCNCVFNCVCRCVBMCVFNSVCMCVCMSU3QmFnZSUyMCUyQiUyMDElN0QlRTUlQjIlODElRTQlQkElODYlMjIp)（需要类型转换）：

```python
age = input("请输入你的年龄：")
age = int(age)  # 将字符串转换为整数
print(f"明年你就{age + 1}岁了")

```

1. 多行输入处理：

```python
print("请输入多行内容（输入空行结束）：")
lines = []
while True:
    line = input()
    if not line:
        break
    lines.append(line)
print("你输入的内容是：")
for line in lines:
    print(line)

```

#### 特点与注意事项

1. 所有输入都以字符串形式返回，如果需要其他数据类型必须进行转换
2. 在 Python 2.x 中，对应的函数是 `raw_input()`
3. 从 Python 3.10 开始，[`input()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md) 函数增加了 `__code__` 等属性
4. 在脚本中使用时，可以配合 `try-except` 处理可能的输入错误

#### 常见应用场景

1. 命令行工具的用户交互
2. 数据收集程序
3. 简单的文本处理工具
4. 教学演示和练习程序
5. 自动化测试中的模拟用户输入

#### 安全提示

当使用 [`input()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md) 接收用户输入时，应当：

* 对输入数据进行验证
* 谨慎处理可能包含恶意代码的输入
* 对于敏感信息（如密码），应考虑使用 `getpass` 模块

[`input()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.input.md) 函数是 Python 中最基础也最常用的交互方式之一，掌握它的使用对 Python 编程非常重要。

---

> 《[Python 的内置函数 input](https://xplanc.online/81de9f2f680a482d0c207d5934dca5e1c437b4def9f46c0121be5f0c1759e684)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148836904)。