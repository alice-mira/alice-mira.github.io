---
title: Python的内置函数print
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 print](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)

Python 的内置函数 [`print()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 是编程中最常用的输出函数之一，主要用于将指定的内容输出到标准输出设备（通常是控制台）。它的基本语法如下：

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)

```

**参数详解：**

1. `*objects`：可接收多个对象参数，会依次打印这些对象。例如：  
```python  
print("Hello", "World")  # 输出：Hello World  
```
2. `sep`：指定多个对象之间的分隔符，默认为一个空格。例如：  
```python  
print("2023", "08", "15", sep="-")  # 输出：2023-08-15  
```
3. `end`：指定输出末尾的字符，默认为换行符 `\n`。例如：  
```python  
print("Hello", end="!!!")  # 输出：Hello!!!（不换行）  
```
4. `file`：指定输出目标，默认为 `sys.stdout`（标准输出）。可以将输出重定向到文件：  
```python  
with open("output.txt", "w") as f:  
    print("Save to file", file=f)  
```
5. `flush`：控制是否强制刷新输出缓冲区，默认为 `False`。设置为 `True` 时会立即输出内容：  
```python  
print("Loading", end="", flush=True)  # 立即显示，不缓冲  
```

**格式化输出示例：**

* 使用 f-string（Python 3.6+）：  
```python  
name = "Alice"  
print(f"Hello, {name}!")  # 输出：Hello, Alice!  
```
* 使用 [`format()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.format.md) 方法：  
```python  
print("Value: {:.2f}".format(3.14159))  # 输出：Value: 3.14  
```

**应用场景：**

1. 调试程序时打印变量值
2. 显示程序运行进度或状态信息
3. 生成格式化报告或日志
4. 交互式命令行程序的输出

**注意事项：**

* 在 Python 2 中 [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 是语句而非函数，写法为 [`print "Hello"`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)
* 大量使用 [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 可能会影响性能，生产环境中建议使用日志模块

---

> 《[Python 的内置函数 print](https://xplanc.online/c9d4cad2d947bf5ad3a227e9441d84625706f18ca1fcfc4d05859550e7f236ae)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149079304)。