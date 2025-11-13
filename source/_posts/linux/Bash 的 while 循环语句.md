---
title: Bash 的 while 循环语句
tags: [linux,bash]
date: 2025-11-10 08:08:08
---

# [#](#999d29)[Bash 的 while 循环语句](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/05.while%20%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5.md#999d29)

Bash 的 while 循环语句的语法为：

```bash
while 条件命令
do
    命令
    ...
done

```

**只要条件为真，就执行循环**。

其中，条件命令返回成功（0）时为真（true），返回失败（非 0）时为假（false）。

如果省略（部分）换行，则需要使用分号（`;`）区分：

```bash
while 条件命令; do 命令; 命令; done

```

示例：

```bash
number=0
while [ "$number" -lt 10 ]  # 只要 "$number" 小于 10，就循环执行
do
    echo "$number"
    number=$((number + 1))
done

```

* 循环打印并增加变量 `number` 的值

运行结果：

```text
0
1
2
3
4
5
6
7
8
9

```

## [#](#2b0183)[break 和 continue 命令](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/05.while%20%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5.md#2b0183)

[`break`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.break.md) 和 [`continue`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.continue.md) 是 Bash 的内置命令，用于跳出循环。

* [`break`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.break.md) 命令立即终止整个循环，继续执行循环之后的命令
* [`continue`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.continue.md) 命令立即结束本轮循环，开始执行下一轮循环

示例：

```bash
number=0
while true # 一直循环执行
do
    if [ "$number" -eq 10 ]  # number 等于 10 时结束循环
    then
        break    # 结束循环
    fi

    if [ "$number" -eq 4 ]  # number 等于 4 时加 3 并跳过本轮循环
    then
        number=$((number + 3))
        continue    # 进入下一轮循环
    fi

    echo "$number"
    number=$((number + 1))
done

```

* `number` 等于 10 时结束循环
* `number` 等于 4 时加 3 并跳过本轮循环

运行结果：

```text
0
1
2
3
7
8
9

```

---

> 《[Bash 的 while 循环语句](https://xplanc.online/12d2acf62063ec73b06bd2265e55c7ad5e40965ef257b71fb015aa35a7677332)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/02.%E8%AF%AD%E6%B3%95/05.while%20%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5.md)。