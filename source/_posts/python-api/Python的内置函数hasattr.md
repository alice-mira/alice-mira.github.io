---
title: Python的内置函数hasattr
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 hasattr](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hasattr.md)

Python 的内置函数 [`hasattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hasattr.md) 用于检查一个对象是否具有指定的属性或方法。该函数的语法为：

```python
hasattr(object, name)

```

参数说明：

* [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)：要检查的对象，可以是任何 Python 对象
* `name`：要检查的属性或方法名称，以字符串形式传入

返回值：

* 如果对象具有该属性或方法，返回 `True`
* 否则返回 `False`

功能特点：

1. 该函数会在对象及其继承链中查找指定属性
2. 对于动态创建的属性同样有效
3. 可以检查方法是否存在，但不会验证方法是否可调用

典型应用场景：

1. [动态属性检查](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBNeUNsYXNzJTNBJTBBJTIwJTIwJTIwJTIwZGVmJTIwX19pbml0X18oc2VsZiklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLnZhbHVlJTIwJTNEJTIwNDIlMEElMEFvYmolMjAlM0QlMjBNeUNsYXNzKCklMEFwcmludChoYXNhdHRyKG9iaiUyQyUyMCd2YWx1ZScpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMFRydWUlMEFwcmludChoYXNhdHRyKG9iaiUyQyUyMCdub25fZXhpc3RlbnQnKSklMjAlMjAlMjMlMjAlRTglQkUlOTMlRTUlODclQkElM0ElMjBGYWxzZQ%3D%3D)：在不确定对象是否具有某个属性时使用

```python
class MyClass:
    def __init__(self):
        self.value = 42

obj = MyClass()
print(hasattr(obj, 'value'))  # 输出: True
print(hasattr(obj, 'non_existent'))  # 输出: False

```

1. [插件系统开发](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hasattr.md)：检查插件是否实现了必需的方法

```python
class Plugin:
    def execute(self):
        pass

plugin = Plugin()
if hasattr(plugin, 'execute'):
    plugin.execute()

```

1. [接口兼容性检查](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hasattr.md)：在调用方法前验证其是否存在

```python
def process(obj):
    if hasattr(obj, 'save'):
        obj.save()
    else:
        print("对象不支持保存操作")

```

注意事项：

1. 与 [`getattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 配合使用可以更安全地访问属性
2. 对于私有属性（以双下划线开头），需要使用真实的名称进行检查
3. 该函数不会触发属性描述符的 `__get__` 方法

对比其他相关函数：

* [`getattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md)：获取属性值，可以设置默认值
* [`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md)：设置属性值
* [`dir()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dir.md)：列出对象的所有属性和方法

性能考虑：  
[`hasattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hasattr.md) 的调用开销相对较小，但在性能敏感的环境中频繁使用仍需谨慎。

---

> 《[Python 的内置函数 hasattr](https://xplanc.online/37c8f12d4dbe0efa066247dd6edbdfeb89edef23e42f13c07bcfc8c4aad06e1f)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148816839)。