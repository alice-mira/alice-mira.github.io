---
title: Python的内置函数exec
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 exec](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.exec.md)

Python 的内置函数 [`exec`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.exec.md) 是一个强大的动态执行工具，它允许程序在运行时执行以字符串形式提供的 Python 代码。

```python
def eval(source:str|codeobject, /, globals:dict=None, locals:mapping=None):
    '''
    执行表达式并返回结果

    :param source: Python 表达式
    :param globals : 全局命名空间字典
    :param locals : 局部命名空间字典
    :return: 表达式的求值结果
    '''

```

[示例](https://xplanc.org/shift/?lang=python&code=ZXhlYyglMjJwcmludCgnaGVsbG8lMjB3b3JsZCcpJTIyKQ%3D%3D)

```python
exec("print('hello world')")

```

重要提示：虽然 [`exec`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.exec.md) 功能强大，但不当使用可能导致严重的安全漏洞。在生产环境中使用时要格外谨慎，特别是处理外部输入时。

安全注意事项：

1. [`exec()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.exec.md) 可以执行任意代码，存在严重的安全风险
2. 永远不要直接执行来自不可信来源的输入

典型应用场景：

1. 数学表达式计算器
2. 配置参数解析
3. 简单脚本执行

---

> 《[Python 的内置函数 exec](https://xplanc.online/65c9a809e4bd02f60c7237b154eb0d966297130b21e0e9fd722eede77e8943e5)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148704058)。