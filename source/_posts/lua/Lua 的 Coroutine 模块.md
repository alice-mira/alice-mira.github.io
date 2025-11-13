---
title: Lua 的 Coroutine 模块
tags: [lua, coroutine]
date: 2025-11-13 08:08:08
---

# [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#eb79b4)[Lua 的 Coroutine 模块](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#eb79b4)

请查看 [Lua 标准库模块列表](https://xplanc.org/primers/document/zh/09.Lua/90.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C.md/01.Lua%20API%20%E7%9B%AE%E5%BD%95.md#b07e50) 了解更多相关 API。 

| 函数                                                                                                                                           | 说明              |
| -------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| [coroutine.create](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7)      | 创建协程对象          |
| [coroutine.close ](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#3f5d4f)      | 关闭协程对象          |
| [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a)      | 恢复协程            |
| [coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264)       | 让出协程            |
| [coroutine.wrap](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#96eca7)        | 创建协程对象，返回一个恢复函数 |
| [coroutine.isyieldable](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#c3e09d) | 检查协程能否让出        |
| [coroutine.running](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#6a2182)     | 获取正在运行的协程对象     |
| [coroutine.status](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#43900b)      | 获取协程状态          |

Lua 支持协同程序（也称为协作多线程）。Lua 中的协程代表一个独立的执行线程。与多线程系统中的线程不同，协程不能被抢占，只能通过显式调用 [coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264) 函数来主动让出。

通过调用 [coroutine.create](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7) 函数创建协程。它的唯一参数是协程的入口函数；[coroutine.create](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7) 函数仅创建一个新的协程并返回该对象，而不会启动该协程。

通过调用 [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a) 函数来执行协程。首次调用时，它的第一个参数是 [coroutine.create](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7) 返回的协程对象，之后的参数传递给协程入口函数。

通过调用 [coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264) 函数来让出协程。让出时 [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a) 返回 [`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md) 和 [coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264) 的所有参数。

让出状态下的协程可以调用 [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a) 来恢复执行。协程恢复时从此前让出时调用 [coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264) 函数的位置继续执行，[coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264) 返回 [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a) 除了第一个参数以外的所有参数。

协程入口函数结束时，其返回值从 [coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a) 返回，该协程无法再次启动，需要调用 [coroutine.close ](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#3f5d4f) 函数进行关闭。

示例

```lua
-- 定义函数，作为协程的入口函数
function coMain(x, y)
    print("co-body", x, y)
    x,y = coroutine.yield(x + y) -- 让出协程
    print("co-body", x, y)
    x,y = coroutine.yield(x + y) -- 让出协程
    print("co-body", x, y)
    return 'end'                 -- 结束
end

-- 创建协程
local co = coroutine.create(coMain)

-- 多次启动协程
print("main", coroutine.resume(co, 1, 10))
print("main", coroutine.resume(co, 5, 9))
print("main", coroutine.resume(co, 3, 7))
print("main", coroutine.resume(co, 9, 9))

```

运行代码

>>> Establishing WebAssembly Runtime. 

>>> Standby. 

Powered by [Shift](https://xplanc.org/shift/#lang=lua&code=LS0lMjAlRTUlQUUlOUElRTQlQjklODklRTUlODclQkQlRTYlOTUlQjAlRUYlQkMlOEMlRTQlQkQlOUMlRTQlQjglQkElRTUlOEQlOEYlRTclQTglOEIlRTclOUElODQlRTUlODUlQTUlRTUlOEYlQTMlRTUlODclQkQlRTYlOTUlQjAlMEFmdW5jdGlvbiUyMGNvTWFpbih4JTJDJTIweSklMEElMjAlMjAlMjAlMjBwcmludCglMjJjby1ib2R5JTIyJTJDJTIweCUyQyUyMHkpJTBBJTIwJTIwJTIwJTIweCUyQ3klMjAlM0QlMjBjb3JvdXRpbmUueWllbGQoeCUyMCUyQiUyMHkpJTIwLS0lMjAlRTglQUUlQTklRTUlODclQkElRTUlOEQlOEYlRTclQTglOEIlMEElMjAlMjAlMjAlMjBwcmludCglMjJjby1ib2R5JTIyJTJDJTIweCUyQyUyMHkpJTBBJTIwJTIwJTIwJTIweCUyQ3klMjAlM0QlMjBjb3JvdXRpbmUueWllbGQoeCUyMCUyQiUyMHkpJTIwLS0lMjAlRTglQUUlQTklRTUlODclQkElRTUlOEQlOEYlRTclQTglOEIlMEElMjAlMjAlMjAlMjBwcmludCglMjJjby1ib2R5JTIyJTJDJTIweCUyQyUyMHkpJTBBJTIwJTIwJTIwJTIwcmV0dXJuJTIwJ2VuZCclMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjAtLSUyMCVFNyVCQiU5MyVFNiU5RCU5RiUwQWVuZCUwQSUwQS0tJTIwJUU1JTg4JTlCJUU1JUJCJUJBJUU1JThEJThGJUU3JUE4JThCJTBBbG9jYWwlMjBjbyUyMCUzRCUyMGNvcm91dGluZS5jcmVhdGUoY29NYWluKSUwQSUwQS0tJTIwJUU1JUE0JTlBJUU2JUFDJUExJUU1JTkwJUFGJUU1JThBJUE4JUU1JThEJThGJUU3JUE4JThCJTBBcHJpbnQoJTIybWFpbiUyMiUyQyUyMGNvcm91dGluZS5yZXN1bWUoY28lMkMlMjAxJTJDJTIwMTApKSUwQXByaW50KCUyMm1haW4lMjIlMkMlMjBjb3JvdXRpbmUucmVzdW1lKGNvJTJDJTIwNSUyQyUyMDkpKSUwQXByaW50KCUyMm1haW4lMjIlMkMlMjBjb3JvdXRpbmUucmVzdW1lKGNvJTJDJTIwMyUyQyUyMDcpKSUwQXByaW50KCUyMm1haW4lMjIlMkMlMjBjb3JvdXRpbmUucmVzdW1lKGNvJTJDJTIwOSUyQyUyMDkpKQ%3D%3D).

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7)[coroutine.create](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fb24e7)

```text
coroutine.create (f)

```

说明

创建一个新的协程，返回该协程对象。

参数

* `f` \- 协程的入口函数

返回值

* 返回创建的协程对象

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#3f5d4f)[coroutine.close](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#3f5d4f)

```text
coroutine.close (co)

```

说明

关闭对象。

参数

* `co` \- 要关闭的协程，必须处于暂停（让出）或死亡（结束）状态

返回值

* 是（[`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md)）否（[`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)）成功

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a)[coroutine.resume](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#76c72a)

```text
coroutine.resume (co [, val1, ···])

```

说明

启动或继续执行协程，不能用于已经死亡（结束）的协程。

参数

* `co` \- 要执行的协程
* `val1, ...` \- 传递给协程的参数，启动时传递给协程入口函数，恢复时通过 [`coroutine.yield`](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md) 返回

返回值

* 正常情况下返回 [`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md) 和 [`coroutine.yield`](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md) 的参数
* 出错时返回 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264)[coroutine.yield](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#f71264)

```text
coroutine.yield (···)

```

说明

让出（暂停）当前协程的执行。

参数

* `...` \- 通过 [`coroutine.resume`](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md) 返回

返回值

* 正常情况下返回 [`coroutine.resume`](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md) 的额外参数

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#96eca7)[coroutine.wrap](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#96eca7)

```text
coroutine.wrap (f)

```

说明

创建一个新的协程，返回该协程的恢复函数，每次调用该函数时都会恢复该协程。

参数

* `f` \- 协程的入口函数

返回值

* 协程的恢复函数

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#c3e09d)[coroutine.isyieldable](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#c3e09d)

```text
coroutine.isyieldable ([co])

```

说明

判断协程是否可以让出。

参数

* `co` \- 要判断的协程；默认值为正在运行的协程

返回值

* 可以让出时返回 [`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md)
* 不可让出时返回 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#6a2182)[coroutine.running](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#6a2182)

```text
coroutine.running ()

```

说明

获取正在运行的协程对象。

参数

无

返回值

* 返回正在运行的协程对象及该协程是（[`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md)）否（[`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)）是主协程

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#43900b)[coroutine.status](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#43900b)

```text
coroutine.status (co)

```

说明

获取协程的状态。

| 状态          | 说明                                  |
| ----------- | ----------------------------------- |
| "running"   | 协程正在运行                              |
| "suspended" | 协程被挂起（未启动或被 yield 让出）               |
| "normal"    | 协程处于活动状态但并非正在运行（该协程中 resume 了另一个协程） |
| "dead"      | 协程死亡（入口函数已经结束）                      |

参数

* `co` \- 要检查的协程

返回值

* 字符串形式的协程状态

## [#](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md#fac4c8)

[Coroutine Manipulation - Lua 5.4 Reference Manual](https://www.lua.org/manual/5.4/manual.html#6.2)

---

> 《[Lua 的 Coroutine 模块](https://xplanc.online/4a97f995e199cd61825e0b53be551b489df6b61d1d5169f398b770fb1debc979)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/09.Lua/92.%E5%86%85%E7%BD%AE%E6%A8%A1%E5%9D%97/EX.coroutine-module.md)。