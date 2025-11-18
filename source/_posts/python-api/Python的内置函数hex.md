---
title: Python的内置函数hex
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 hex](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md)

Python 的内置函数 [`hex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md) 用于将一个整数转换为以 “0x” 为前缀的小写十六进制字符串。该函数接受一个整数作为参数，并返回对应的十六进制字符串表示。

#### 详细说明

1. **函数语法**：  
```python  
hex(x)  
```  
   * `x`：必须是一个整数对象（可以是 Python 的 [`int`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 类型，或者实现了 `__index__()` 方法的自定义对象）
2. **返回值**：  
   * 返回字符串类型，格式为 `"0x"` 开头，后面跟随十六进制数字（a-f 使用小写字母）  
   * 例如：[`hex(255)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md) 返回 `'0xff'`
3. **参数要求**：  
   * 如果传入非整数对象（如浮点数），会抛出 `TypeError` 异常  
   * 对于负数，返回其补码形式的十六进制表示
4. **[示例用法](https://xplanc.org/shift/?lang=python&code=cHJpbnQoaGV4KDE2KSklMjAlMjAlMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUEweDEwJTBBcHJpbnQoaGV4KC0xMCkpJTIwJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJUVGJUJDJTlBLTB4YSUwQXByaW50KGhleCgwKSklMjAlMjAlMjAlMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElRUYlQkMlOUEweDAlMEElMEElMjMlMjAlRTglODclQUElRTUlQUUlOUElRTQlQjklODklRTclQjElQkIlRTQlQkQlQkYlRTclOTQlQTglMjBfX2luZGV4X18lMjAlRTYlOTYlQjklRTYlQjMlOTUlMEFjbGFzcyUyME15TnVtYmVyJTNBJTBBJTIwJTIwJTIwJTIwZGVmJTIwX19pbmRleF9fKHNlbGYpJTNBJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwcmV0dXJuJTIwMTAwJTBBcHJpbnQoaGV4KE15TnVtYmVyKCkpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSVFRiVCQyU5QTB4NjQ%3D)**：  
```python  
print(hex(16))    # 输出：0x10  
print(hex(-10))   # 输出：-0xa  
print(hex(0))     # 输出：0x0  
# 自定义类使用 __index__ 方法  
class MyNumber:  
    def __index__(self):  
        return 100  
print(hex(MyNumber()))  # 输出：0x64  
```
5. **应用场景**：  
   * 内存地址显示  
   * 颜色代码转换（RGB 转十六进制）  
   * 低级编程和硬件相关操作  
   * 数据校验和哈希值展示
6. **注意事项**：  
   * 若要转换为大写十六进制，可以结合 `upper()` 方法：[`hex(255).upper()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md)  
   * 与 [`int()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 函数配合可以实现十六进制字符串和整数之间的相互转换  
   * 从 Python 3.8 开始，[`int`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 类型也提供了 [`hex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md) 方法：[`(255).hex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md)
7. **底层实现**：  
   * 实际调用的是该对象的 `__hex__()` 方法（如果存在）  
   * 对于 [`int`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md) 类型，会直接返回其十六进制字符串表示
8. **相关函数**：  
   * [`bin()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md)：转换为二进制字符串  
   * [`oct()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md)：转换为八进制字符串  
   * [`format()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.format.md)：提供更灵活的格式化选项（如 [`format(255, "#04x")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.format.md)）

这个函数在处理需要十六进制表示的场合非常有用，特别是与底层系统交互或需要展示内存数据时。

---

> 《[Python 的内置函数 hex](https://xplanc.online/75378ad8b592f7c3cca000530105bee8a8107c19adfb8590b696e0f8e7ee01bf)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148834715)。