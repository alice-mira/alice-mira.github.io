---
title: Python的内置函数setattr
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 setattr](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md)

Python 的内置函数 [`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md) 用于动态设置对象的属性值。该函数接受三个参数：对象、属性名称字符串和属性值。当我们需要在运行时为对象添加或修改属性时，[`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md) 提供了灵活的操作方式。

基本语法：

```python
setattr(object, attribute_name, value)

```

详细说明：

1. 参数解析：  
   * [`object`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md)：需要设置属性的目标对象  
   * `attribute_name`：字符串形式的属性名称  
   * `value`：要设置的属性值
2. 功能特点：  
   * 可以动态地为对象添加新属性  
   * 可以修改对象已有属性的值  
   * 属性名称可以通过字符串形式动态指定  
   * 与 [`getattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.getattr.md) 函数形成互补操作
3. 典型应用场景：  
   * 动态配置对象属性（如根据配置文件设置属性）  
   * 在元编程中动态修改类或实例  
   * 实现类似字典的访问接口  
   * 批量设置多个属性

[示例代码](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBQZXJzb24lM0ElMEElMjAlMjAlMjAlMjBwYXNzJTBBJTBBcCUyMCUzRCUyMFBlcnNvbigpJTBBJTBBJTIzJTIwJUU4JUFFJUJFJUU3JUJEJUFFJUU1JThEJTk1JUU0JUI4JUFBJUU1JUIxJTlFJUU2JTgwJUE3JTBBc2V0YXR0cihwJTJDJTIwJ25hbWUnJTJDJTIwJ0FsaWNlJyklMEFwcmludChwLm5hbWUpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBJTNBJTIwQWxpY2UlMEElMEElMjMlMjAlRTYlODklQjklRTklODclOEYlRTglQUUlQkUlRTclQkQlQUUlRTUlQjElOUUlRTYlODAlQTclMEFhdHRyaWJ1dGVzJTIwJTNEJTIwJTdCJ2FnZSclM0ElMjAyNSUyQyUyMCdqb2InJTNBJTIwJ0VuZ2luZWVyJyU3RCUwQWZvciUyMGtleSUyQyUyMHZhbHVlJTIwaW4lMjBhdHRyaWJ1dGVzLml0ZW1zKCklM0ElMEElMjAlMjAlMjAlMjBzZXRhdHRyKHAlMkMlMjBrZXklMkMlMjB2YWx1ZSklMEElMEFwcmludChwLmFnZSUyQyUyMHAuam9iKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMDI1JTIwRW5naW5lZXIlMEElMEElMjMlMjAlRTQlQkYlQUUlRTYlOTQlQjklRTUlQjclQjIlRTYlOUMlODklRTUlQjElOUUlRTYlODAlQTclMEFzZXRhdHRyKHAlMkMlMjAnYWdlJyUyQyUyMDI2KSUwQXByaW50KHAuYWdlKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQSUzQSUyMDI2)：

```python
class Person:
    pass

p = Person()

# 设置单个属性
setattr(p, 'name', 'Alice')
print(p.name)  # 输出: Alice

# 批量设置属性
attributes = {'age': 25, 'job': 'Engineer'}
for key, value in attributes.items():
    setattr(p, key, value)

print(p.age, p.job)  # 输出: 25 Engineer

# 修改已有属性
setattr(p, 'age', 26)
print(p.age)  # 输出: 26

```

注意事项：

1. 属性名称必须是字符串
2. 如果对象是类的实例，属性将作用于实例而非类
3. 与直接使用点号(.)赋值的区别在于属性名称的动态性
4. 对于不可变对象或某些内置类型可能无法设置属性

[`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md) 与 [`object.attribute = value`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.object.md) 的等价关系：

```python
setattr(obj, 'attr', value)  # 等价于
obj.attr = value

```

但 [`setattr()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.setattr.md) 的优势在于属性名称可以是运行时确定的字符串变量，这在需要动态处理属性时特别有用。

---

> 《[Python 的内置函数 setattr](https://xplanc.online/a244c062e71eb47585c13328a230d77fc31ae103f21e77780ab5228840f4c324)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149182303)。