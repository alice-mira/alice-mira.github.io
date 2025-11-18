---
title: Python的内置函数len
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 len](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md)

Python 的内置函数 [`len()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md) 是一个常用的内置函数，主要用于返回对象的长度或项目数量。它可以应用于多种数据类型，包括但不限于以下几种：

1. **字符串（str）**：[返回字符串中的字符数量](https://xplanc.org/shift/?lang=python&code=dGV4dCUyMCUzRCUyMCUyMkhlbGxvJTJDJTIwV29ybGQhJTIyJTBBcHJpbnQobGVuKHRleHQpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QTEz)。例如：  
```python  
text = "Hello, World!"  
print(len(text))  # 输出：13  
```
2. **列表（list）**：[返回列表中元素的数量](https://xplanc.org/shift/?lang=python&code=bnVtYmVycyUyMCUzRCUyMCU1QjElMkMlMjAyJTJDJTIwMyUyQyUyMDQlMkMlMjA1JTVEJTBBcHJpbnQobGVuKG51bWJlcnMpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QTU%3D)。例如：  
```python  
numbers = [1, 2, 3, 4, 5]  
print(len(numbers))  # 输出：5  
```
3. **元组（tuple）**：[返回元组中元素的数量](https://xplanc.org/shift/?lang=python&code=Y29vcmRpbmF0ZXMlMjAlM0QlMjAoMTAlMkMlMjAyMCUyQyUyMDMwKSUwQXByaW50KGxlbihjb29yZGluYXRlcykpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJUVGJUJDJTlBMw%3D%3D)。例如：  
```python  
coordinates = (10, 20, 30)  
print(len(coordinates))  # 输出：3  
```
4. **字典（dict）**：[返回字典中键值对的数量](https://xplanc.org/shift/?lang=python&code=dXNlciUyMCUzRCUyMCU3QiUyMm5hbWUlMjIlM0ElMjAlMjJBbGljZSUyMiUyQyUyMCUyMmFnZSUyMiUzQSUyMDI1JTdEJTBBcHJpbnQobGVuKHVzZXIpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QTI%3D)。例如：  
```python  
user = {"name": "Alice", "age": 25}  
print(len(user))  # 输出：2  
```
5. **集合（set）**：[返回集合中元素的数量](https://xplanc.org/shift/?lang=python&code=dW5pcXVlX251bWJlcnMlMjAlM0QlMjAlN0IxJTJDJTIwMiUyQyUyMDIlMkMlMjAzJTdEJTBBcHJpbnQobGVuKHVuaXF1ZV9udW1iZXJzKSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUEz)。例如：  
```python  
unique_numbers = {1, 2, 2, 3}  
print(len(unique_numbers))  # 输出：3  
```

**注意事项**：

* [`len()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md) 函数只能应用于支持长度计算的对象，否则会引发 `TypeError` 异常。
* 对于自定义的类，可以通过实现 `__len__()` 方法来使其支持 [`len()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md) 函数。例如：  
```python  
class MyCollection:  
    def __len__(self):  
        return 10  
obj = MyCollection()  
print(len(obj))  # 输出：10  
```

**应用场景**：

* 在循环中确定迭代次数。
* 检查集合是否为空（[`len(collection) == 0`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md)）。
* 数据验证时确保长度符合预期。
* 在处理用户输入时验证字符串长度限制。

[`len()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md) 是一个高效且广泛使用的函数，在 Python 编程中扮演着重要角色。

---

> 《[Python 的内置函数 len](https://xplanc.online/21e840b936c926f016c073569a09aec35f531ad75804d52f19cbee678ecdc0ca)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148910516)。