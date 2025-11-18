---
title: Python的内置函数complex
tags: [后端,python,API]
date: 2025-11-18 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 complex](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.complex.md)

Python 的内置函数 [`complex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.complex.md) 用于创建一个复数对象。复数在数学和科学计算中有着广泛的应用，特别是在信号处理、电气工程和物理学等领域。

```python
class complex(r=0, i=0):
    '''
    类型转换为 complex

    :param r: 实部
    :param i: 虚部
    :return: 转换为 complex 后的值
    '''

```

### 示例

```python
# 创建实部为 3，虚部为 5 的复数
c1 = complex(3, 5)  # 输出 (3+5j)

# 仅指定实部
c2 = complex(2)  # 输出 (2+0j)

```

Python 的内置函数 [`complex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.complex.md) 用于创建一个复数对象，或将其他数据类型转换为复数类型。复数在数学和工程计算中非常常见，特别是在信号处理、控制系统等领域。

#### 语法格式：

```python
complex([real[, imag]])

```

或者

```python
complex(string)

```

#### 参数说明：

1. **第一种形式**：  
   * `real`（可选）：表示复数的实部，可以是整数、浮点数或字符串。如果省略，默认为 0。  
   * `imag`（可选）：表示复数的虚部，可以是整数或浮点数。如果省略，默认为 0。
2. **第二种形式**：  
   * `string`：一个表示复数的字符串，例如 `"3+4j"` 或 `"5-2j"`。字符串中不能包含空格，且虚部必须带有 `j` 或 `J` 后缀。

#### 返回值：

返回一个复数对象，其实部和虚部分别为指定的数值。复数对象是不可变类型。

#### 示例说明：

1. **创建简单复数**：  
```python  
a = complex(3, 4)   # 创建复数 3+4j  
print(a)            # 输出：(3+4j)  
print(type(a))      # 输出：<class 'complex'>  
```
2. **省略部分参数**：  
```python  
b = complex(2)      # 创建复数 2+0j（省略虚部）  
c = complex()       # 创建复数 0j（省略实部和虚部）  
d = complex(imag=5) # 创建复数 0+5j（仅指定虚部）  
```
3. **从字符串创建复数**：  
```python  
e = complex("1+2j") # 创建复数 1+2j  
f = complex("3.5")  # 创建复数 3.5+0j（字符串仅包含实部）  
```
4. **复数运算**：  
```python  
x = complex(1, 2)  
y = complex(3, 4)  
print(x + y)        # 复数加法：(4+6j)  
print(x * y)        # 复数乘法：(-5+10j)  
print(abs(y))       # 复数模：5.0  
```

#### 注意事项：

* 如果实部或虚部是字符串形式，它必须是一个合法的数值表达式，不能包含除数字、加减号和 `j` 之外的字符。
* 复数对象支持常见的算术运算，包括加法、减法、乘法和除法。
* 复数对象的实部和虚部可以通过 `real` 和 `imag` 属性获取：  
```python  
z = complex(3, 4)  
print(z.real)  # 输出实部：3.0  
print(z.imag)  # 输出虚部：4.0  
```

#### 应用场景：

复数作为一种重要的数学工具，在多个工程和科学领域都有着深入而广泛的应用，具体包括：

1. **信号处理领域**  
   * 在数字信号处理中，复数被广泛应用于频谱分析和滤波器设计  
   * FFT（快速傅里叶变换）算法完全建立在复数运算的基础上，是音频处理、图像压缩等技术的核心  
   * 例如：MP3音频编码就依赖复数运算进行频域分析和压缩
2. **电气工程领域**  
   * 在交流电路分析中，复数形式的阻抗（Z=R+jX）可以同时表示电阻和电抗  
   * 相量法使用复数表示正弦信号的幅度和相位，简化了电路计算  
   * 典型应用包括：电力系统分析、电机控制、射频电路设计等
3. **量子力学领域**  
   * 量子态用复数概率幅描述，薛定谔方程本身就是复数方程  
   * 复数是量子叠加原理和量子纠缠现象数学描述的基础  
   * 例如：量子计算中的量子比特就是用复数向量表示的
4. **计算机图形学领域**  
   * 复数可以用来表示二维旋转和缩放变换  
   * 四元数（复数的扩展）在三维图形旋转中广泛应用  
   * 实际应用包括：游戏引擎中的角色动画、VR/AR中的空间定位等

此外，复数还在控制理论、流体力学、电磁学等其他多个领域发挥着重要作用，是现代科学技术不可或缺的数学工具。

通过 [`complex()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.complex.md) 函数，Python 可以方便地处理这些需要复数运算的场景。

---

> 《[Python 的内置函数 complex](https://xplanc.online/84d006aefab75887f5e9b4024548f11f5ab0cadfc0dbca91dbc9bbc02cde5427)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148622198)。