---
title: Python的内置函数getattr
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 getattr](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md)

```python
def getattr(obj, name:str):
    '''
    获取属性的值

    :param obj: 一个对象
    :param name: 属性的名字
    '''

```

Python 的内置函数 getattr 是一个非常有用的反射工具，主要用于动态获取对象的属性或方法。其基本语法为：[`getattr(object, name[, default])`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md)，其中 object 是目标对象，name 是属性/方法名称字符串，default 是可选参数，当属性不存在时返回该值而不是抛出 AttributeError。

具体功能和使用场景如下：

1. **基本属性获取**：  
 可以直接[获取对象属性](https://xplanc.org/shift/index.html?lang=python&code=Y2xhc3MlMjBQZXJzb24lM0ElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2luaXRfXyhzZWxmKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHNlbGYubmFtZSUyMCUzRCUyMCUyMkFsaWNlJTIyJTBBcCUyMCUzRCUyMFBlcnNvbigpJTBBcHJpbnQoZ2V0YXR0cihwJTJDJTIwJTIybmFtZSUyMikpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJTIwJTIyQWxpY2UlMjI%3D)，等价于 [`object.name`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 的点号访问方式，但更加动态灵活：  
```python  
class Person:  
    def __init__(self):  
        self.name = "Alice"  
p = Person()  
print(getattr(p, "name"))  # 输出 "Alice"  
```
2. **方法动态调用**：  
 可以获取并[调用对象方法](https://xplanc.org/shift/index.html?lang=python&code=Y2xhc3MlMjBQZXJzb24lM0ElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2luaXRfXyhzZWxmKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHNlbGYubmFtZSUyMCUzRCUyMCUyMkFsaWNlJTIyJTBBJTBBJTIwJTIwJTIwJTIwZGVmJTIwZ3JlZXQoc2VsZiklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBwcmludChmJ2hlbGxvJTIwJTdCc2VsZi5uYW1lJTdEJyklMEElMjAlMjAlMjAlMEFwJTIwJTNEJTIwUGVyc29uKCklMEFtZXRob2QlMjAlM0QlMjBnZXRhdHRyKHAlMkMlMjAlMjJncmVldCUyMiUyQyUyME5vbmUpJTBBaWYlMjBjYWxsYWJsZShtZXRob2QpJTNBJTBBJTIwJTIwJTIwJTIwbWV0aG9kKCk%3D)。这在需要根据运行时条件选择不同方法时特别有用：  
```python  
method = getattr(p, "greet", None)  
if callable(method):  
    method()  
```
3. **默认值处理**：  
 当属性不存在时，可以指定默认返回值而不引发异常：  
```python  
age = getattr(p, "age", 25)  # 如果p没有age属性则返回25  
```

典型应用场景包括：

1. **插件系统开发，动态加载模块和函数**
* 在IDE开发中实现代码提示插件，通过反射动态加载不同语言的分析器
* 游戏引擎中的Mod系统，运行时加载玩家自定义的脚本模块
* 企业级应用的扩展点机制，如ERP系统通过反射加载不同供应商的对接模块
1. **实现类似 switch-case 的功能结构**
* 命令模式解析器，根据输入指令字符串反射调用对应的处理方法
* 状态机实现，通过反射自动匹配状态转换方法
* REST API路由分发，将HTTP方法(GET/POST)和路径映射到控制器方法
1. **配置文件驱动的方法调用**
* 定时任务调度系统，通过配置文件指定要执行的任务类和方法
* 数据转换管道，配置文件中定义转换步骤对应的处理方法
* 自动化测试框架，通过测试用例配置反射调用测试方法
1. **对象序列化/反序列化工具**
* JSON/XML转换库，通过反射分析对象属性进行序列化
* ORM框架，将数据库记录反射映射到实体对象
* 分布式RPC框架，方法参数和返回值的自动序列化
* 深度克隆工具，通过反射递归复制对象所有字段

注意：相比直接访问对象属性（如 `obj.attribute`），使用 [`getattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 函数（如 [`getattr(obj, 'attribute')`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md)）会带来额外的性能开销。这主要是因为：

1. **查找机制差异**：[`getattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 需要通过字符串名称在运行时动态查找属性，涉及额外的哈希计算和字典查找操作。
2. **函数调用成本**：作为内置函数，[`getattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 会产生函数调用的开销，包括参数传递和栈帧创建。
3. **异常处理**：当属性不存在时，[`getattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 默认会抛出 AttributeError，异常处理机制也会消耗资源。

在性能关键场景（如高频循环、实时系统、游戏引擎等）中，建议：

* 优先使用直接属性访问
* 可将频繁访问的属性缓存到局部变量
* 如需动态访问，可考虑预先建立 {name:attr} 的映射字典

示例对比：

```python
# 直接访问（推荐）
value = obj.attr

# 动态访问（灵活但较慢）
value = getattr(obj, 'attr')

```

当确实需要动态属性访问时（如实现插件系统、ORM映射等），[`getattr`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 的灵活性优势可能超过其性能代价。

---

> 《[Python 的内置函数 getattr](https://xplanc.online/3b96d013549e1cea4b0d598e6847cdf34c6fa06922d8df302f939d22e01b8e23)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148752165)。