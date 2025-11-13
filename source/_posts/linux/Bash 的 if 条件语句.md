---
title: Bash 的 if 条件语句
tags: [linux,bash]
date: 2025-11-12 08:08:08
---

# [#](#403d7c)[Bash 的 if 条件语句](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/04.if%20%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5.md#403d7c)

Bash 的 if 条件语句的语法为：

```bash
if 条件命令
then
    命令
    ...
elif 条件命令
then
    命令
    ...
else
    命令
    ...
fi

```

其中，条件命令返回成功（0）时为真（true），返回失败（非 0）时为假（false）。

如果省略（部分）换行，则需要使用分号（`;`）区分：

```bash
if 条件命令; then 命令; 命令; elif 条件命令; then 命令; 命令; else 命令; 命令; fi

```

示例：

```bash
if test "$SHELL" = "/bin/bash"
then
    echo 很好
else
    echo 完蛋
fi

```

* 判断变量 `SEHLL` 的值是否是 `/bin/bash`

注意，这里的 `"$SHELL" = "/bin/bash"` 不要省略引号写成 `$SHELL = /bin/bash`；否则变量 `SHELL` 为空时会产生语法错误。

* `=` \- 判断字符串相等
* `!=` \- 判断字符串不同

## [#](#50302b)[test 命令](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/04.if%20%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5.md#50302b)

如上述示例代码，Bash 的条件一般使用 [`test`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.test.md) 命令，格式为：

```bash
test 条件表达式

[ 条件表达式 ]      # 不可省略空格

[[ 条件表达式 ]]    # 不可省略空格

```

* [`test`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.test.md) 和 `[` 是等价的，它们既是 Bash 的内置命令，也是可执行文件
* `[[` 是 Bash 的关键字，额外支持正则判断

[`test`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.test.md) 命令的常用选项如下：

* `-e` \- 文件存在
* `-f` \- 文件存在且是普通文件
* `-d` \- 文件存在且是目录
* `-b` \- 文件存在且是块设备
* `-c` \- 文件存在且是字符设备
* `-L` \- 文件存在且是符号链接
* `-eq` \- 等于（只能用于整数，下同）
* `-ne` \- 不等于
* `-lt` \- 小于
* `-le` \- 小于或等于
* `-gt` \- 大于
* `-ge` \- 大于或等于

例如：

```bash
FILE="$0"

if [ -f $FILE ]; then
    echo $FILE 是普通文件
elif [ -e $FILE ]; then
    echo $FILE 不是普通文件
else
    echo $FILE 文件不存在
fi

```

运行代码

>>> Establishing WebAssembly Runtime. 

>>> Standby. 

Powered by [Shift](https://xplanc.org/shift/#lang=bash&code=RklMRSUzRCUyMiUyNDAlMjIlMEElMEFpZiUyMCU1QiUyMC1mJTIwJTI0RklMRSUyMCU1RCUzQiUyMHRoZW4lMEElMjAlMjAlMjAlMjBlY2hvJTIwJTI0RklMRSUyMCVFNiU5OCVBRiVFNiU5OSVBRSVFOSU4MCU5QSVFNiU5NiU4NyVFNCVCQiVCNiUwQWVsaWYlMjAlNUIlMjAtZSUyMCUyNEZJTEUlMjAlNUQlM0IlMjB0aGVuJTBBJTIwJTIwJTIwJTIwZWNobyUyMCUyNEZJTEUlMjAlRTQlQjglOEQlRTYlOTglQUYlRTYlOTklQUUlRTklODAlOUElRTYlOTYlODclRTQlQkIlQjYlMEFlbHNlJTBBJTIwJTIwJTIwJTIwZWNobyUyMCUyNEZJTEUlMjAlRTYlOTYlODclRTQlQkIlQjYlRTQlQjglOEQlRTUlQUQlOTglRTUlOUMlQTglMEFmaQ%3D%3D).

## [#](#72d684)[true 和 false](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/04.if%20%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5.md#72d684)

Bash 的内置命令中包含 [`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md) 和 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md) 两个命令，前者直接返回成功（0），后者直接返回失败（1）。

---

> 《[Bash 的 if 条件语句](https://xplanc.online/206bc24117bb76a69c544823337bc25b2d56df675eed39e29b2244e25abee012)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/04.if%20%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5.md)。