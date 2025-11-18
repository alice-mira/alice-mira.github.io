---
title: Python的内置函数set
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 set](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md)

Python 的内置函数 [`set()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md) 是一个非常有用的数据结构，用于创建无序且不包含重复元素的集合。它提供了高效的成员检测和元素去重功能，是处理集合运算的理想选择。

#### 基本用法

1. **创建集合**：  
```python  
# 使用花括号  
fruits = {'apple', 'banana', 'orange'}  
# 使用set()函数  
numbers = set([1, 2, 3, 2, 1])  # 结果为{1, 2, 3}  
```
2. **空集合创建**：  
```python  
empty_set = set()  # 注意：不能使用{}，这会创建字典  
```

#### 主要特性

* **无序性**：集合中的元素没有固定顺序
* **唯一性**：自动去除重复元素
* **可变性**：可以添加/删除元素
* **可迭代性**：可以使用for循环遍历

#### 常用操作

1. **添加元素**：  
```python  
s = {1, 2}  
s.add(3)  # {1, 2, 3}  
s.update([4, 5])  # {1, 2, 3, 4, 5}  
```
2. **删除元素**：  
```python  
s.remove(2)  # 如果元素不存在会报错  
s.discard(2)  # 元素不存在不会报错  
s.pop()  # 随机删除并返回一个元素  
```
3. **集合运算**：  
```python  
a = {1, 2, 3}  
b = {2, 3, 4}  
# 并集  
a.union(b)  # {1, 2, 3, 4}  
# 交集  
a.intersection(b)  # {2, 3}  
# 差集  
a.difference(b)  # {1}  
# 对称差集  
a.symmetric_difference(b)  # {1, 4}  
```

#### 应用场景

1. **数据去重**：  
```python  
lst = [1, 2, 2, 3, 3, 3]  
unique = set(lst)  # {1, 2, 3}  
```
2. **快速成员检测**：  
```python  
if user_input in valid_options:  
    # 比列表检测更高效  
```
3. **关系运算**：  
```python  
# 检查两个用户的好友列表是否有交集  
common_friends = user1_friends & user2_friends  
```

#### 注意事项

* 集合只能包含可哈希（不可变）对象
* 不能通过索引访问元素
* 冻结集合（frozenset）是集合的不可变版本
* 集合在Python 3.7+中会保留插入顺序，但不应该依赖这个特性

集合是Python中处理唯一值集合的高效工具，合理使用可以显著提升代码性能和简洁性。Python 的内置函数 set

---

> 《[Python 的内置函数 set](https://xplanc.online/170ca1f1a603a6c799184953a66c06f7eb2171260528bed2354bba6f0a85d406)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/149138325)。