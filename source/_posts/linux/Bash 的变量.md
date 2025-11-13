---
title: Bash 的变量
tags: [linux,bash]
---

# [#](#def1d8)[Bash 的变量](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#def1d8)

Bash 中的变量定义语法如下：

```bash
变量名=值

```

注意，等号（`=`）两边不能有空格。

变量名的命名应当遵循如下规则：

* 只能包含**字母**，**数字**和**下划线（`_`）**，并且不能以数字开头。
* 不能使用 Bash 保留的关键字，如：`if` `then` `else` `fi` `for` `while` `do` `done` 等
* 环境变量和常量使用全大写字母，单词间使用下划线分隔
* 普通变量使用全小写字母，单词间使用下划线分隔
* 函数内的局部变量使用 `local` 关键字声明

例如：

```bash
PI=3.1415925
URL="https://xplanc.org/"

```

## [#](#fe6da5)[读取变量](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#fe6da5)

在 Bash 中通过美元符号（`$`）将变量名解析为值。格式为：

```bash
$变量名

# 或

${变量名}

```

例如：

```bash
>>> PI=3.1415925
>>> echo PI
PI
>>> echo $PI
3.1415925

```

## [#](#ba6b00)[删除变量](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#ba6b00)

使用 `unset` 命令可以删除变量。格式为为：

```bash
unset 变量名

```

## [#](#3a9da6)[运算](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#3a9da6)

在 Bash 中进行运算需要使用 `$(( 表达式 ))`。例如：

```bash
>>> echo $(( 1 + 1 ))
2
>>> a=10
>>> b=3
>>> echo $(( $a / $b ))
3

```

* 注意，仅支持整数运算

## [#](#ae27b4)[环境变量](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#ae27b4)

Bash 在运行可执行文件时，会创建一个新的进程并重置全部的环境。因此该程序无法读取到之前 Bash 上创建的变量。

如果需要一个变量可以被可执行文件读取，则需要使用 [`export`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.export.md) 命令创建环境变量。格式为：

```bash
export 变量名=值

```

可以通过 [`env`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.env.md) 命令查看当前存在的全部环境变量：

```bash
$ env
SHELL=/bin/bash
NVM_RC_VERSION=
PWD=/home/planc
LOGNAME=planc
XDG_SESSION_TYPE=tty
HOME=/home/planc
LANG=en_US.UTF-8
...

```

## [#](#bb7ece)[特殊变量](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md#bb7ece)

Bash 中预设了一批特殊变量，这些变量只能读取，不能被赋值。

* `$?` \- 一个命令的退出码，通常使用 `0` 表示成功，非 `0` 表示失败
* `$$` \- 当前 Shell 的 ID
* `$0` \- 当前命令，直接读取时是 Bash 自身，在脚本中读取时是脚本文件
* `$1` \- 当前命令的第一个参数，`$2`，`$3` 以此类推
* `$#` \- 当前命令的参数数量
* `$@` \- 当前命令的全部参数

---

> 《[Bash 的变量](https://xplanc.online/4e781c51ab0006c992bfbde1826732fc2c3a711111318f2c41964c594e2611be)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/02.%E5%8F%98%E9%87%8F.md)。