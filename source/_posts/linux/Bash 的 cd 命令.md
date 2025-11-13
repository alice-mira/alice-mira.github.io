---
title: Bash 的 cd 命令
tags: [linux,bash,cd]
---

# [#](#f51e00)[Bash 的 cd 命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md#f51e00)

```text
cd [-L|-P] [DIRECTORY]

```

功能

切换工作目录。

类型

Bash 内置命令。

参数

* `OPTION` 选项：  
   * `-L` \- 逻辑路径；在跟踪符号链接之前解析 `..`（默认）  
   * `-P` \- 物理路径；在跟踪符号链接之后解析 `..`
* `DIRECTORY` \- 要切换到的目录路径；省略表示切换到用户目录，`-` 表示切换到上次的工作目录

## [#](#0d53f0)[示例](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md#0d53f0)

基本示例

```shell
$ pwd                       # 查看当前路径
/home/user/primers
$ cd bash                   # 相对路径
$ pwd 
/home/user/primers/bash
$ cd -                      # 切换回之前的目录
$ pwd 
/home/user/primers
$ cd /etc                   # 绝对路径
$ pwd 
/etc

```

符号链接

```shell
$ pwd                       # 查看当前路径
/home/user/primers
$ ln -s /usr/lib lib        # 创建符号链接
$ cd lib                    # 进入 lib
$ pwd 
/home/user/primers/bash/lib
$ cd ..                     # 返回上级目录
$ cd -P lib                 # 进入 lib，跟踪符号链接
$ pwd 
/usr/lib

```

## [#](#f837e2)[相关命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md#f837e2)

| 命令                                                                                                          | 说明                  |
| ----------------------------------------------------------------------------------------------------------- | ------------------- |
| [pushd](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.pushd.md) | 将当前工作目录压入栈顶，并切换工作目录 |
| [popd](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.popd.md)   | 将目录栈的栈顶移除，并切换工作目录   |
| [dirs](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.dirs.md)   | 查看当前工作目录和目录栈        |

## [#](#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md#fac4c8)

* [cd(1p) — Linux manual page](https://www.man7.org/linux/man-pages/man1/cd.1p.html)

## [#](#5fe4e2)[手册](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md#5fe4e2)

---

> 《[Bash 的 cd 命令](https://xplanc.online/19b24d39aea18f1c224054e90dba3d75c12e0cc41a190689679d34771692432e)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md)。