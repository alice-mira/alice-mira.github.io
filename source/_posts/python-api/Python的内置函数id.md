---
title: Python的内置函数id
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 id](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.id.md)

Python 的内置函数 [`id()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.id.md) 是一个非常有用的工具函数，它返回一个对象的"身份标识"，这个标识实际上是该对象在内存中的地址（以整数形式表示）。以下是关于 [`id()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.id.md) 函数的详细说明：

1. **[基本用法](https://xplanc.org/shift/?lang=python&code=eCUyMCUzRCUyMDQyJTBBcHJpbnQoaWQoeCkpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJUU0JUI4JTgwJUU0JUI4JUFBJUU2JTk1JUI0JUU2JTk1JUIwJUVGJUJDJThDJUU0JUJCJUEzJUU4JUExJUE4JUU1JThGJTk4JUU5JTg3JThGeCVFNiU4OSU4MCVFNSVCQyU5NSVFNyU5NCVBOCVFNyU5QSU4NCVFNSVBRiVCOSVFOCVCMSVBMSVFNyU5QSU4NCVFNSU4NiU4NSVFNSVBRCU5OCVFNSU5QyVCMCVFNSU5RCU4MA%3D%3D)**  
```python  
x = 42  
print(id(x))  # 输出一个整数，代表变量x所引用的对象的内存地址  
```
2. **特性说明**  
   * 每个对象在内存中都有唯一的id  
   * 这个id在对象的生命周期内保持不变  
   * 不同对象可能有相同的id（如果前一个对象已被销毁）
3. **内存管理关联**  
   * 小整数（-5到256）在Python中会被缓存，因此相同值的小整数通常具有相同的id  
   * 对于较大的整数或可变对象，即使值相同，id通常也不同
4. **应用场景**  
   * 调试时检查两个变量是否引用同一个对象  
   * 理解Python的可变和不可变对象的行为差异  
   * 探究Python的内存管理机制
5. **[示例对比](https://xplanc.org/shift/?lang=python&code=YSUyMCUzRCUyMDI1NiUwQWIlMjAlM0QlMjAyNTYlMEFwcmludChpZChhKSUyMCUzRCUzRCUyMGlkKGIpKSUyMCUyMCUyMyUyMFRydWUlRUYlQkMlOEMlRTUlOUIlQTAlRTQlQjglQkElRTUlQjAlOEYlRTYlOTUlQjQlRTYlOTUlQjAlRTclQkMlOTMlRTUlQUQlOTglMEElMEFjJTIwJTNEJTIwNjU1MzUlMEFkJTIwJTNEJTIwNjU1MzUlMEFwcmludChpZChjKSUyMCUzRCUzRCUyMGlkKGQpKSUyMCUyMCUyMyUyMEZhbHNlJUVGJUJDJThDJUU4JUI2JTg1JUU1JTg3JUJBJUU3JUJDJTkzJUU1JUFEJTk4JUU4JThDJTgzJUU1JTlCJUI0)**  
```python  
a = 256  
b = 256  
print(id(a) == id(b))  # True，因为小整数缓存  
c = 257  
d = 257  
print(id(c) == id(d))  # False，超出缓存范围  
```
6. **注意事项**  
   * 不要将id值用于持久化存储，因为每次程序运行时id可能不同  
   * id()的结果是依赖于实现的，不同Python解释器可能有不同表现  
   * 在CPython中，id()返回的就是对象的内存地址
7. **与is运算符的关系**  
`a is b` 实际上等价于 [`id(a) == id(b)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.id.md)，都是检查两个变量是否引用同一个对象

理解[`id()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.id.md)函数可以帮助开发者更好地掌握Python的对象模型和内存管理机制，对于编写高效、正确的Python代码很有帮助。

---

> 《[Python 的内置函数 id](https://xplanc.online/1f56deebba681f96cde27aec3b0953d9d7dad44e395dd2b511c932e992e67d91)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148836899)。