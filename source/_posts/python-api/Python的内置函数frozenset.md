---
title: Python的内置函数frozenset
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 frozenset](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md)

```python
def frozenset(x):
    '''
    类型转换为 frozenset

    :param x: 一个变量
    :return: 转换为 frozenset 后的值
    '''

```

Python 的内置函数 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 用于创建一个不可变的集合对象，它继承了普通集合（[`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md)）的所有特性，如无序性、元素唯一性等，但关键区别在于 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 一旦创建就不能被修改，因此它是可哈希的（hashable）。这使得 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 可以作为字典的键或其他集合的元素，而普通的可变集合（[`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md)）则不具备这种能力。

#### 主要特性

1. **不可变性**：与 [`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md) 不同，[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 不能通过 `add()`、`remove()` 等方法修改其内容。尝试修改会引发 `AttributeError`。
2. **[可哈希性](https://xplanc.org/shift/index.html?lang=python&code=ZnMlMjAlM0QlMjBmcm96ZW5zZXQoJTVCMSUyQyUyMDIlMkMlMjAzJTVEKSUwQWQlMjAlM0QlMjAlN0JmcyUzQSUyMCUyMnZhbHVlJTIyJTdEJTIwJTIwJTIzJTIwJUU1JTkwJTg4JUU2JUIzJTk1JUU2JTkzJThEJUU0JUJEJTlD)**：由于不可变，[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 可哈希，可以作为字典的键或另一个集合的元素。例如：  
```python  
fs = frozenset([1, 2, 3])  
d = {fs: "value"}  # 合法操作  
```
3. **支持集合操作**：[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 支持所有集合操作，如并集（`|`）、交集（`&`）、差集（`-`）等，但这些操作会返回新的 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 对象而非修改原对象。

#### 创建方式

[通过 frozenset() 构造函数创建](https://xplanc.org/shift/index.html?lang=python&code=ZnMxJTIwJTNEJTIwZnJvemVuc2V0KCU1QjElMkMlMjAyJTJDJTIwMyU1RCklMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjMlMjAlRTQlQkIlOEUlRTUlODglOTclRTglQTElQTglRTUlODglOUIlRTUlQkIlQkElMEFmczIlMjAlM0QlMjBmcm96ZW5zZXQoJTIyaGVsbG8lMjIpJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIzJTIwJUU0JUJCJThFJUU1JUFEJTk3JUU3JUFDJUE2JUU0JUI4JUIyJUU1JTg4JTlCJUU1JUJCJUJBJUVGJUJDJTg4JUU1JTg1JTgzJUU3JUI0JUEwJUU0JUI4JUJBJUU1JUFEJTk3JUU3JUFDJUE2JUVGJUJDJTg5JTBBZnMzJTIwJTNEJTIwZnJvemVuc2V0KCklMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjMlMjAlRTclQTklQkElMjBmcm96ZW5zZXQ%3D)，参数可以是任何可迭代对象（如列表、元组、字符串等）。若未提供参数，则返回空 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md)。

```python
fs1 = frozenset([1, 2, 3])       # 从列表创建
fs2 = frozenset("hello")         # 从字符串创建（元素为字符）
fs3 = frozenset()                # 空 frozenset

```

#### 典型应用场景

1. **字典的键**：当需要集合作为键时，必须使用 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md)。  
```python  
graph = {  
    frozenset(["A", "B"]): 10,  
    frozenset(["B", "C"]): 5,  
}  
```
2. **集合的元素**：嵌套集合时，内部集合必须是 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md)。  
```python  
s = {frozenset([1, 2]), frozenset([3, 4])}  
```
3. **数据去重与缓存**：在需要缓存集合结果或确保数据不可篡改的场景中使用。

#### 示例对比

```python
# 可变集合（set）的局限性
s = {1, 2}
d = {s: "error"}  # TypeError: unhashable type: 'set'

# 使用 frozenset 解决
fs = frozenset(s)
d = {fs: "valid"}  # 成功

```

[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 的出现丰富了集合的应用场景[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) ，尤其是在需要不可变性和可哈希性的场景中。

[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md)是 Python 中不可变集合的实现，它的存在大大扩展了集合的应用范围。与普通 [`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md) 相比，[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 具有以下几个重要特点和优势：

1. **作为字典键**：由于 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 是不可变的，它可以被用作字典的键，而普通 [`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md) 则不行。这在需要建立集合到值的映射时特别有用。  
```python  
valid = frozenset(['name', 'age'])  
data = {valid: 'user_info'}  
```
2. **集合元素**：[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 可以作为其他集合的元素，而普通 [`set`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md) 不能。  
```python  
s = {frozenset([1,2]), frozenset([3,4])}  
```
3. **缓存优化**：由于 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 不可变，可以安全地进行缓存和重用，提高性能。
4. **线程安全**：在多线程环境中，[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 的不可变性保证了线程安全。
5. **数学运算**：在需要进行集合运算但又不希望原始集合被修改的场景下，[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 是完美的选择。
6. **数据验证**：可以用作常量集合来验证数据，确保集合内容不会被意外修改。

[`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 支持所有集合的操作（如 `union`、`intersection` 等），但不会修改自身，而是返回新的 [`frozenset`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.frozenset.md) 对象。这一特性使其在函数式编程范式下特别有价值。

---

> 《[Python 的内置函数 frozenset](https://xplanc.online/90a06f3afd6f1b3540adb103236cd51903bcce0cf54a8a453a8e2cbf459c0a04)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148752109)。