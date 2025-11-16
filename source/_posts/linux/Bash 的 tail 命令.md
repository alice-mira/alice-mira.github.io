---
title: Bash 的 tail 命令
tags: [linux,bash,cd]
date: 2025-11-16 02:33:09
---

# [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#f4f325)[Bash 的 tail 命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#f4f325)

```bash
tail [OPTION]... [FILE]...

```

**功能**

查看文件的末尾。

**类型**

可执行文件（[`/usr/bin/tail`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md)），属于 [coreutils](https://www.gnu.org/software/coreutils/)。

**参数**

* `OPTION` 选项：  
   * `-c`, `--bytes=[+]NUM` \- 查看文件末尾的 `NUM` 字节，如果使用正号，则表示查看第 `NUM` 字节之后的内容  
   * `-f`, `--follow[={name|descriptor}]` \- 跟随文件，当文件内容增加时打印追加的内容  
   * `-F` \- 等价于 `--follow=name --retry`  
   * `-n`, `--lines=[+]NUM` \- 查看文件末尾的 `NUM` 行，如果使用正号，则表示查看第 `NUM` 行之后的内容  
   * `--max-unchanged-stats=N` \- 使用 `-f` 选项选项时，如果连续 `N` 次读取文件不变，则尝试重新打开文件  
   * `--pid=PID` \- 使用 `-f` 选项选项时，当 `PID` 进程结束时停止此命令  
   * [`-q`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.q.md), `--quiet`, `--silent` \- 不打印包含文件名在内的头部信息  
   * `--retry` \- 如果文件无法打开，则重新尝试打开  
   * `-v`, `--verbose` \- 打印包含文件名在内的头部信息  
   * `-z`, `--zero-terminated` \- 以空字符（`\0`）作为行的结尾，而不是换行符（`\n`）  
   * `--help` \- 显示帮助  
   * `--version` \- 显示版本
* `FILE` \- 文件列表，如果没有这个参数或指定为 `-`，则读取标准输入

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#0d53f0)[示例](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#0d53f0)

**基本功能**

```shell
$ man tail | tail -n 5                  # 查看末尾 5 行

       Full documentation <https://www.gnu.org/software/coreutils/tail>
       or available locally via: info '(coreutils) tail invocation'

GNU coreutils 9.4                 April 2024                           TAIL(1)
$ man tail | tail -n +90                # 显示第 90 行之后的内容
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       head(1)

       Full documentation <https://www.gnu.org/software/coreutils/tail>
       or available locally via: info '(coreutils) tail invocation'

GNU coreutils 9.4                 April 2024                           TAIL(1)

```

**监听日志**

```shell
$ tail -f /var/log/syslog       # 监听该文件，文件内容更新时打印追加的内容
2025-11-15T08:30:00.190259+00:00 dev systemd[1]: Finished sysstat-collect.service - system activity accounting tool.
2025-11-15T08:35:01.817178+00:00 dev CRON[3239701]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
2025-11-15T08:40:00.422316+00:00 dev systemd[1]: Starting sysstat-collect.service - system activity accounting tool...
2025-11-15T08:40:00.435212+00:00 dev systemd[1]: sysstat-collect.service: Deactivated successfully.
2025-11-15T08:40:00.435761+00:00 dev systemd[1]: Finished sysstat-collect.service - system activity accounting tool.
2025-11-15T08:45:01.832707+00:00 dev CRON[3241555]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
2025-11-15T08:50:00.422442+00:00 dev systemd[1]: Starting sysstat-collect.service - system activity accounting tool...
2025-11-15T08:50:00.434650+00:00 dev systemd[1]: sysstat-collect.service: Deactivated successfully.
2025-11-15T08:50:00.435219+00:00 dev systemd[1]: Finished sysstat-collect.service - system activity accounting tool.
2025-11-15T08:55:01.848254+00:00 dev CRON[3243092]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)


```

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#f837e2)[相关命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#f837e2)

| 命令                                                                                                        | 说明          |
| --------------------------------------------------------------------------------------------------------- | ----------- |
| [head](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.head.md) | 查看文件开头      |
| [more](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.more.md) | 分页查看文件内容    |
| [less](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.less.md) | 增强版文件分页阅读命令 |

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#fac4c8)

* [Output the last part of files - GNU Coreutils](https://www.gnu.org/software/coreutils/manual/html%5Fnode/tail-invocation.html)
* [tail(1) — Linux manual page](https://www.man7.org/linux/man-pages/man1/tail.1.html)

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#5fe4e2)[手册](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md#5fe4e2)

### 显示

```text
TAIL(1)                          User Commands                         TAIL(1)

NAME
       tail - output the last part of files

SYNOPSIS
       tail [OPTION]... [FILE]...

DESCRIPTION
       Print  the  last  10  lines of each FILE to standard output.  With more
       than one FILE, precede each with a header giving the file name.

       With no FILE, or when FILE is -, read standard input.

       Mandatory arguments to long options are  mandatory  for  short  options
       too.

       -c, --bytes=[+]NUM
              output  the  last  NUM  bytes; or use -c +NUM to output starting
              with byte NUM of each file

       -f, --follow[={name|descriptor}]
              output appended data as the file grows;

              an absent option argument means 'descriptor'

       -F     same as --follow=name --retry

       -n, --lines=[+]NUM
              output the last NUM lines, instead of the last  10;  or  use  -n
              +NUM to skip NUM-1 lines at the start

       --max-unchanged-stats=N
              with --follow=name, reopen a FILE which has not

              changed  size  after  N  (default 5) iterations to see if it has
              been unlinked or renamed (this is the usual case of rotated  log
              files); with inotify, this option is rarely useful

       --pid=PID
              with -f, terminate after process ID, PID dies

       -q, --quiet, --silent
              never output headers giving file names

       --retry
              keep trying to open a file if it is inaccessible

       -s, --sleep-interval=N
              with -f, sleep for approximately N seconds (default 1.0) between
              iterations;  with  inotify and --pid=P, check process P at least
              once every N seconds

       -v, --verbose
              always output headers giving file names

       -z, --zero-terminated
              line delimiter is NUL, not newline

       --help display this help and exit

       --version
              output version information and exit

       NUM may have a multiplier suffix: b 512, kB 1000, K 1024, MB 1000*1000,
       M 1024*1024, GB 1000*1000*1000, G 1024*1024*1024, and so on for  T,  P,
       E,  Z, Y, R, Q.  Binary prefixes can be used, too: KiB=K, MiB=M, and so
       on.

       With --follow (-f), tail defaults to  following  the  file  descriptor,
       which  means that even if a tail'ed file is renamed, tail will continue
       to track its end.  This default behavior is not desirable when you  re‐
       ally want to track the actual name of the file, not the file descriptor
       (e.g.,  log  rotation).   Use  --follow=name in that case.  That causes
       tail to track the named file in a way that accommodates  renaming,  re‐
       moval and creation.

AUTHOR
       Written  by Paul Rubin, David MacKenzie, Ian Lance Taylor, and Jim Mey‐
       ering.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright © 2023 Free Software Foundation, Inc.   License  GPLv3+:  GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       head(1)

       Full documentation <https://www.gnu.org/software/coreutils/tail>
       or available locally via: info '(coreutils) tail invocation'

GNU coreutils 9.4                 April 2024                           TAIL(1)

```

---

> 《[Bash 的 tail 命令](https://xplanc.online/e34454419ab3c5fa55787bbe58c94e09448357d8b8425e35e2b85f088c1ac9e1)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md)。