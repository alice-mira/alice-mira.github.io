---
title: Lua 的 Math 模块
tags: [lua, math]
date: 2025-11-13 08:08:08
---

# [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#750363)[Lua 的 Math 模块](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#750363)

请查看 [Lua 标准库模块列表](https://xplanc.org/primers/document/zh/09.Lua/90.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C.md/01.Lua%20API%20%E7%9B%AE%E5%BD%95.md#b07e50) 了解更多相关 API。 

| 常量              | 说明                                                                                                                                              |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| math.huge       | 数值的最大值，通常对应 C 语言中的 [HUGE\_VAL](https://xplanc.org/primers/document/zh/06.C/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.math.h.md#7dc406)   |
| math.maxinteger | 整数的最大值，通常对应 C 语言中的 [LONG\_MAX](https://xplanc.org/primers/document/zh/06.C/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.limits.h.md#d2ecd2) |
| math.mininteger | 整数的最小值，通常对应 C 语言中的 [LONG\_MIN](https://xplanc.org/primers/document/zh/06.C/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.limits.h.md#d2ecd2) |
| math.pi         | 圆周率                                                                                                                                             |

| 函数                                                                                                                               | 说明                |
| -------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| [math.max](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#5ba713)       | 取最大值              |
| [math.min](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#55fce0)       | 取最小值              |
| [math.ceil](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#a67ed2)      | 向上取整              |
| [math.floor](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#437992)     | 向下取整              |
| [math.modf](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cb4d5b)      | 分解整数部分和小数部分（向零取整） |
| [math.fmod](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cd8bc9)      | 计算除法的余数           |
| [math.deg](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#f9d2fb)       | 弧度转角度             |
| [math.rad](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#e2410d)       | 角度转弧度             |
| [math.abs](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#0370fb)       | 计算绝对值             |
| [math.acos](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b109e3)      | 计算反余弦             |
| [math.asin](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#08053e)      | 计算反正弦             |
| [math.atan](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#416f37)      | 计算反正切             |
| [math.cos](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#903215)       | 计算余弦              |
| [math.sin](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b6752f)       | 计算余弦              |
| [math.tan](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#09af5c)       | 计算正切              |
| [math.exp](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3f5736)       | 计算自然常数  的幂        |
| [math.log](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#58954a)       | 计算对数              |
| [math.sqrt](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#36559d)      | 计算平方根             |
| [math.tointeger](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#2c2a52) | 转换为整数             |
| [math.type](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#01f7b6)      | 检查类型              |
| [math.ult](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3639a5)       | 比较无符号整数大小         |

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#0370fb)[math.abs](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#0370fb)

```text
math.abs (x)

```

说明

计算 `x` 的绝对值。

参数

* `x` \- 一个数值

返回值

* 返回 `x` 的绝对值

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b109e3)[math.acos](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b109e3)

```text
math.acos (x)

```

说明

计算 `x` 的反余弦。

参数

* `x` \- 弧度

返回值

* 返回 `x` 的反余弦

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#08053e)[math.asin](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#08053e)

```text
math.asin (x)

```

说明

计算 `x` 的反正弦。

参数

* `x` \- 弧度

返回值

* 返回 `x` 的反正弦

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#416f37)[math.atan](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#416f37)

```text
math.atan (y [, x])

```

说明

计算 `y/x` 的反正切。

参数

* `y` \- 弧度的分子
* `x` \- 弧度的分母；默认为 1

返回值

* 返回 `y/x` 的反正切

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#a67ed2)[math.ceil](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#a67ed2)

```text
math.ceil (x)

```

说明

将 `x` 向上取整，返回大于或等于 `x` 的最小整数值。

参数

* `x` \- 一个数值

返回值

* 返回大于或等于 `x` 的最小整数值

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#903215)[math.cos](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#903215)

```text
math.cos (x)

```

说明

计算 `x` 的余弦。

参数

* `x` \- 弧度

返回值

* 返回 `x` 的余弦

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#f9d2fb)[math.deg](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#f9d2fb)

```text
math.deg (x)

```

说明

将弧度 `x` 转换为角度。

参数

* `x` \- 弧度

返回值

* 返回弧度 `x` 对应的角度

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3f5736)[math.exp](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3f5736)

```text
math.exp (x)

```

说明

计算自然常数 `e` 的 `x` 次方。

参数

* `x` \- 指数

返回值

* 返回

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#437992)[math.floor](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#437992)

```text
math.floor (x)

```

说明

将 `x` 向下取整，返回小于或等于 `x` 的最大整数值。

参数

* `x` \- 一个数值

返回值

* 返回小于或等于 `x` 的最大整数值

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cd8bc9)[math.fmod](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cd8bc9)

```text
math.fmod (x, y)

```

说明

计算 `x` 除以 `y` 的余数，其中商的部分向 0 取整。

参数

* `x` \- 被除数
* `y` \- 除数

返回值

* 返回 `x` 除以 `y` 的余数

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#58954a)[math.log](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#58954a)

```text
math.log (x [, base])

```

说明

计算以 `base` 为底，`x` 的对数（）。

参数

* `x` \- 真数
* `base` \- 底数；默认为自然常数

返回值

* 返回以 `base` 为底，`x` 的对数

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#5ba713)[math.max](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#5ba713)

```text
math.max (x, ···)

```

说明

取最大值。

参数

* `x` \- 数值
* `...` \- 数值

返回值

* 返回参数中的最大值

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#55fce0)[math.min](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#55fce0)

```text
math.min (x, ···)

```

说明

取最小值。

参数

* `x` \- 数值
* `...` \- 数值

返回值

* 返回参数中的最小值

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cb4d5b)[math.modf](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#cb4d5b)

```text
math.modf (x)

```

说明

分离数值的整数部分和小数部分。

参数

* `x` \- 要处理的数值

返回值

* 返回整数部分和小数部分

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#e2410d)[math.rad](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#e2410d)

```text
math.rad (x)

```

说明

将角度 `x` 转换为弧度。

参数

* `x` \- 要转换的角度

返回值

* 返回角度 `x` 对应的弧度

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b6752f)[math.sin](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#b6752f)

```text
math.sin (x)

```

说明

计算 `x` 的正弦。

参数

* `x` \- 弧度

返回值

* 返回 `x` 的正弦

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#36559d)[math.sqrt](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#36559d)

```text
math.sqrt (x)

```

说明

计算 `x` 的平方根。

参数

* `x` \- 被开方数

返回值

* 返回 `x` 的平方根

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#09af5c)[math.tan](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#09af5c)

```text
math.tan (x)

```

说明

计算 `x` 的正切。

参数

* `x` \- 弧度

返回值

* 返回 `x` 的正切

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#2c2a52)[math.tointeger](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#2c2a52)

```text
math.tointeger (x)

```

说明

将变量 `x` 转换为整数。

参数

* `x` \- 要被转换的变量

返回值

* 成功时返回对应的整数值
* 失败时返回 `nil`

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#01f7b6)[math.type](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#01f7b6)

```text
math.type (x)

```

说明

检查变量 `x` 的数值类型。

参数

* `x` \- 要检查的变量

返回值

* `x` 是整数时返回 `"integer"`
* `x` 是小数时返回 `"float"`
* `x` 不是数值时返回 `nil`

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3639a5)[math.ult](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#3639a5)

```text
math.ult (m, n)

```

说明

判断无符号整数 `m` 是否小于无符号整数 `n`。

* 如果 `m` 或 `n` 是有符号整数，则会被转换为无符号整数
* 如果 `m` 或 `n` 不是整数，则会报错

参数

* `m` \- 要比较的无符号整数
* `n` \- 要比较的无符号整数

返回值

* `m` `n` 时返回 `true`
* 否则返回 `false`

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md#fac4c8)

[Mathematical Manipulation - Lua 5.4 Reference Manual](https://www.lua.org/manual/5.4/manual.html#6.7)

---

> 《[Lua 的 Math 模块](https://xplanc.online/ccf4cdc1747f956e0035d5bb0ad20acdaf415e788e46880f902da55f639e52c8)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.math-module.md)。