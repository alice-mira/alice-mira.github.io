---
title: Python的内置函数globals
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 globals](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md)

Python 的内置函数 [`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 是一个非常重要的工具函数，它返回一个字典，表示当前全局符号表。这个字典包含了当前模块中定义的所有全局变量、函数和类的名称及其对应的值。

```python
def globals():
    '''
    返回实现当前模块命名空间的字典

    :return: 当前模块命名空间的字典
    '''

```

具体来说：

1. 返回值是一个字典对象
2. 字典的键是变量名或函数名（字符串形式）
3. 字典的值是对应的对象引用
4. 修改这个字典会直接影响全局命名空间

典型应用场景包括：

* 动态访问或修改全局变量
* 调试时查看当前全局状态
* 框架开发中实现动态功能

[示例用法](https://xplanc.org/shift/?lang=python&code=eCUyMCUzRCUyMDEwJTBBeSUyMCUzRCUyMCUyMmhlbGxvJTIyJTBBJTBBZGVmJTIwZnVuYygpJTNBJTBBJTIwJTIwJTIwJTIwcGFzcyUwQSUwQSUyMyUyMCVFOCU4RSVCNyVFNSU4RiU5NiVFNSU4NSVBOCVFNSVCMSU4MCVFNSU4RiU5OCVFOSU4NyU4RiVFNSVBRCU5NyVFNSU4NSVCOCUwQWclMjAlM0QlMjBnbG9iYWxzKCklMEElMEElMjMlMjAlRTglQUUlQkYlRTklOTclQUUlRTUlODUlQTglRTUlQjElODAlRTUlOEYlOTglRTklODclOEYlMEFwcmludChnJTVCJTIyeCUyMiU1RCklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElM0ElMjAxMCUwQXByaW50KGclNUIlMjJ5JTIyJTVEKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMCUyMmhlbGxvJTIyJTBBJTBBJTIzJTIwJUU0JUJGJUFFJUU2JTk0JUI5JUU1JTg1JUE4JUU1JUIxJTgwJUU1JThGJTk4JUU5JTg3JThGJTBBZyU1QiUyMnglMjIlNUQlMjAlM0QlMjAyMCUwQXByaW50KHgpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJTNBJTIwMjAlMEElMEElMjMlMjAlRTYlQjclQkIlRTUlOEElQTAlRTYlOTYlQjAlRTUlODUlQTglRTUlQjElODAlRTUlOEYlOTglRTklODclOEYlMEFnJTVCJTIyeiUyMiU1RCUyMCUzRCUyMCU1QjElMkMlMjAyJTJDJTIwMyU1RCUwQXByaW50KHopJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJTNBJTIwJTVCMSUyQyUyMDIlMkMlMjAzJTVE)：

```python
x = 10
y = "hello"

def func():
    pass

# 获取全局变量字典
g = globals()

# 访问全局变量
print(g["x"])  # 输出: 10
print(g["y"])  # 输出: "hello"

# 修改全局变量
g["x"] = 20
print(x)  # 输出: 20

# 添加新全局变量
g["z"] = [1, 2, 3]
print(z)  # 输出: [1, 2, 3]

```

注意事项：

1. 在函数内部使用时，[`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 仍然返回模块级的全局变量，而不是函数的局部变量。例如：

```python
x = 10  # 全局变量
def test():
    y = 20  # 局部变量
    print(globals())  # 输出包含x但不包含y
test()

```

这个特性与 `local()` 形成鲜明对比，后者在函数内部调用时会返回函数的局部命名空间。

1. 与 [`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 不同，[`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 的一个重要特点是它的行为具有一致性：无论在任何位置调用（模块级、函数内部、类方法中等），它都返回相同的结果 - 即当前模块的全局命名空间。例如：

```python
def outer():
    def inner():
        print(globals())  # 与模块级调用结果相同
    inner()
outer()

```

这种可预测的行为使得 [`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 比 [`locals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.locals.md) 更适合在嵌套环境中使用。

1. 虽然 [`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 提供了便利的全局变量访问方式，但过度使用可能会使代码变得难以维护：
* 它会破坏代码的封装性，使得函数不再自包含
* 可能导致难以追踪的变量修改
* 增加代码的耦合度  
 建议仅在以下场景谨慎使用：

```python
# 合理的使用示例：动态配置
CONFIG = {'debug': True}

def process_data():
    if globals().get('CONFIG', {}).get('debug'):
        print("Debug mode enabled")

```

在其他情况下，更推荐使用显式的参数传递或类属性访问。

在框架开发中，[`globals()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.globals.md) 常用于实现插件系统或动态加载功能，允许在运行时注册新的全局对象。

---

> 《[Python 的内置函数 globals](https://xplanc.online/bf79c733ae69bfa00e4d0b49d12d696b532de3b1935c75f4e4baf8866d752b9c)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148800680)。