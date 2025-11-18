---
title: Python的内置函数all
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 all](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.hide/EX.all.md)

all() 是 Python 提供的一个高效工具，它可以快速判断可迭代对象中的所有元素是否都为真值（Truthy）。它的使用非常简单，但结合不同的场景，可以写出非常优雅的代码。

all 的函数原型如下：

```python
def all(iterable):
    '''
    判断可迭代对象内容是否全部为真值

    :param iterable: 一个可迭代对象
    :return: 如果 iterable 的所有元素均为真值则返回 True，否则返回 False；如果 iterable 是空的，返回 True
    '''

```

### 示例

[在线运行](https://xplanc.org/shift/#lang=python&input=&code=cHJpbnQoYWxsKCU1QiU1RCkpJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIzJTIwJUU3JUE5JUJBJUU3JTlBJTg0JUU1JThGJUFGJUU4JUJGJUFEJUU0JUJCJUEzJUU1JUFGJUI5JUU4JUIxJUExJUU4JUJGJTk0JUU1JTlCJTlFJTIwVHJ1ZSUwQSUwQXByaW50KGFsbChyYW5nZSgxMCkpKSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMyUyMDAuLi45JTBBcHJpbnQoYWxsKHJhbmdlKDElMkMlMjAxMCkpKSUyMCUyMCUyMCUyMCUyMyUyMDEuLi45)

```python
print(all([]))              # 空的可迭代对象返回 True

print(all(range(10)))       # 0...9
print(all(range(1, 10)))    # 1...9

```

all() 函数，它能够高效地检查一个可迭代对象中的所有元素是否都为真值。通过示例代码，我们看到了它在数据验证、条件判断等场景下的强大能力。

---

> 《[Python 的内置函数 all](https://xplanc.online/f84c659567b28f4e3d52ee92288b4433128433d309fa1683c5549a84ea24621b)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148503359)。