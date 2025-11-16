---
title: Python的内置函数locals
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 locals](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md)

Python 的内置函数 [`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 是一个非常有用的工具函数，它返回一个字典，包含当前局部命名空间中的所有变量名及其对应的值。这个字典反映了函数或代码块中当前可访问的所有局部变量。

```python
def locals():
    '''
    返回一个代表当前局部符号表的映射对象

    :return: 当前局部符号表的映射对象
    '''

```

#### 功能详解：

1. **返回内容**：[`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 返回的字典包含当前作用域中定义的所有局部变量，包括：  
   * 函数内部定义的变量  
   * 循环中的临时变量  
   * 通过赋值语句创建的变量
2. **动态性**：值得注意的是，当修改返回的字典时，实际上也会影响当前作用域中的变量值。不过这种行为在不同 Python 实现中可能有所差异，官方文档建议不要依赖这种修改行为。
3. **与 globals() 的区别**：  
   * [`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 返回局部命名空间  
   * [`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 返回全局命名空间  
   * 在模块级别调用时，两者返回的内容相同

#### 典型应用场景：

1. **[调试时查看变量](https://xplanc.org/shift/?lang=python&code=ZGVmJTIwY2FsY3VsYXRpb24oeCUyQyUyMHkpJTNBJTBBJTIwdGVtcCUyMCUzRCUyMHglMjAqJTIweSUwQSUyMHByaW50KGxvY2FscygpKSUyMCUyMCUyMyUyMCVFNiU5RiVBNSVFNyU5QyU4QiVFNSVCRCU5MyVFNSU4OSU4RCVFNiU4OSU4MCVFNiU5QyU4OSVFNSVCMSU4MCVFOSU4MyVBOCVFNSU4RiU5OCVFOSU4NyU4RiUwQSUyMHJldHVybiUyMHRlbXAlMjAlMkIlMjAxMDAlMEElMEFjYWxjdWxhdGlvbigxJTJDJTIwMik%3D)**：  
```python  
def calculation(x, y):  
 temp = x * y  
 print(locals())  # 查看当前所有局部变量  
 return temp + 100  
calculation(1, 2)  
```

#### 注意事项：

* 在函数内部，[`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 只包含函数开始执行后定义的变量
* 在类方法中，不会包含实例属性（self.xxx）
* 由于性能考虑，CPython 的实现可能不会实时更新返回的字典

[`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 函数为 Python 程序员提供了一种强大的自省(introspection)能力，在调试、元编程和动态代码生成等场景中非常实用。

---

> 《[Python 的内置函数 locals](https://xplanc.online/7fb55b2e5f6005b9b8a7915d53ac2bca0d9d9d29b073f5d5ee79ee6db11c8c80)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148937670)。