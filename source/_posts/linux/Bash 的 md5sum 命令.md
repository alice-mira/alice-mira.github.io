---
title: Bash 的 md5sum 命令
tags: [linux,bash,md5sum]
date: 2025-11-11 08:08:08
---


# [#](#eece16)[Bash 的 md5sum 命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md#eece16)

```text
md5sum [OPTION]... [FILE]...

```

功能

计算或校验 MD5 值。

类型

可执行文件（[`/usr/bin/md5sum`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md)），属于 [coreutils](https://www.gnu.org/software/coreutils/)。

参数

* `OPTION` 选项：  
   * [`-b`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.b.md), `--binary` \- 以二进制模式读取文件；类 UNIX 系统下始终是二进制模式  
   * `-c`, `--check` \- 从文件中读取 MD5 值进行校验  
   * `--tag`\- 生成 BSD 风格的输出  
   * `-t`, `--text` \- 以文本模式读取文件；类 UNIX 系统下不存在文本模式，此选项无效  
   * `-z`, `--zero` \- 以空字符（`\0`）作为行的结尾，而不是换行符（`\n`）  
   * `--ignore-missing` \- 校验时忽略缺失的文件  
   * `--quiet` \- 校验时不打印成功的消息  
   * `--status` \- 校验时不打印任何消息；可以通过返回值检查是否成功  
   * `--strict` \- 校验时严格检查格式  
   * `-w`, `--warn` \- 校验时遇到格式不正确的行时产生警告  
   * `--help` \- 显示帮助  
   * `--version` \- 显示版本
* `FILE` \- 文件列表

## [#](#0d53f0)[示例](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md#0d53f0)

计算 MD5 值

```shell
$ md5sum 1.txt                                   # 单个文件
79171af5e65e23a97b58c343c4de7411  1.txt
$ md5sum 1.txt 2.txt 3.txt                       # 多个文件
79171af5e65e23a97b58c343c4de7411  1.txt
d68dae595d597fb67c85a8301521b097  2.txt
72d93867588107cf46b2cc7ea400d0aa  3.txt
$ md5sum --tag 1.txt 2.txt 3.txt                 # BSD 风格
MD5 (1.txt) = 79171af5e65e23a97b58c343c4de7411
MD5 (2.txt) = d68dae595d597fb67c85a8301521b097
MD5 (3.txt) = 72d93867588107cf46b2cc7ea400d0aa

```

校验 MD5 值

```shell
$ md5sum 1.txt 2.txt 3.txt > md5.txt
$ md5sum -c md5.txt # 校验
1.txt: OK
2.txt: OK
3.txt: OK

```

## [#](#f837e2)[相关命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md#f837e2)

| 命令                                                                                                                  | 说明             |
| ------------------------------------------------------------------------------------------------------------------- | -------------- |
| [b2sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.b2sum.md)         | 计算和校验 BLAKE2 值 |
| [sha1sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sha1sum.md)     | 计算和校验 SHA1 值   |
| [sha224sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sha224sum.md) | 计算和校验 SHA224 值 |
| [sha256sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sha256sum.md) | 计算和校验 SHA256 值 |
| [sha384sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sha384sum.md) | 计算和校验 SHA384 值 |
| [sha512sum](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sha512sum.md) | 计算和校验 SHA512 值 |

## [#](#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md#fac4c8)

* [Print or check MD5 digests - GNU Coreutils](https://www.gnu.org/software/coreutils/manual/html%5Fnode/md5sum-invocation.html)
* [md5sum(1) — Linux manual page](https://www.man7.org/linux/man-pages/man1/md5sum.1.html)

## [#](#5fe4e2)[手册](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md#5fe4e2)

---

> 《[Bash 的 md5sum 命令](https://xplanc.online/1067ab193e2a839d69ff54b3a2e4feeedc206264b7d2c53cac7e10966f2b9182)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.md5sum.md)。