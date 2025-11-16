---
title: Bash 的 chown 命令
tags: [linux,bash,cd]
date: 2025-11-16 02:26:08
---

# [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#1c21ea)[Bash 的 chown 命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#1c21ea)

```text
chown [OPTION]... [OWNER][:[GROUP]] FILE...

```

功能

修改文件的所有者和所属组。

类型

可执行文件（[`/usr/bin/chown`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md)），属于 [coreutils](https://www.gnu.org/software/coreutils/)。

参数

* `OPTION` 选项：  
   * `-c`, `--changes` \- 仅对发生变化的文件打印详细信息  
   * `-f`, `--silent`, `--quiet` \- 忽略大部分错误信息  
   * `-v`, `--verbose` \- 打印详细信息  
   * `--dereference` \- 影响符号链接引用的源文件，而非符号链接本身（默认）  
   * `-h`, `--no-dereference` \- 影响符号链接本身，而不是其引用的源文件  
   * `--from=CURRENT_OWNER:CURRENT_GROUP` \- 仅当文件的所有者和所属主是 `CURRENT_OWNER` 和 `CURRENT_GROUP` 才进行修改  
   * `--no-preserve-root` \- 不保护 `/` 目录  
   * `--preserve-root` \- 保护 `/` 目录  
   * `--reference=RFILE` \- 引用 `RFILE` 文件的配置  
   * `-R`, `--recursive` \- 对目录进行递归操作  
   * `-H` \- 使用 `-R` 选项进行递归操作时，指向目录的符号链接只有作为命令行参数时才遍历  
   * `-L` \- 使用 `-R` 选项进行递归操作时，遍历所有指向目录的符号链接  
   * `-P` \- 使用 `-R` 选项进行递归操作时，不遍历任何符号链接（默认）  
   * `--help` \- 显示帮助  
   * `--version` \- 显示版本
* `OWNER` \- 要设为的所有者
* `GROUP` \- 要设为的所属组
* `FILE` \- 文件列表

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#0d53f0)[示例](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#0d53f0)

用户名或组名

```shell
$ chown planc file.txt                  # 将 file 的所有者设为 planc
$ chown :primers file.txt               # 将 file 的所属组设为 primers
$ chown planc:primers file.txt          # 将 file 的所有者设为 planc 所属组设为 primers

```

用 ID 或组 ID

```shell
$ chown 1001 file.txt                   # 将 file 的所有者 ID 设为 1001
$ chown :1001 file.txt                  # 将 file 的所属组 ID 设为 1001
$ chown 1001:1001 file.txt              # 将 file 的所有者 ID 设为 1001 所属组 ID 设为 1001

```

其它

```shell
$ chown --reference=2.txt 1.txt         # 将 1.txt 的所有者和所属组设为和 2.txt 一样
$ chown planc:primers -R dir            # 递归设置目录 dir 中的文件

```

修改根目录（危险！）

```shell
$ chown planc --no-preserve-root -R /   # 危险！千万不要执行此命令！

```

修改系统关键文件的所有者可能导致系统无法启动，请谨慎操作。 

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#f837e2)[相关命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#f837e2)

| 命令                                                                                                          | 说明        |
| ----------------------------------------------------------------------------------------------------------- | --------- |
| [chgrp](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chgrp.md) | 修改文件的所属组  |
| [chmod](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md) | 修改文件的访问权限 |

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#fac4c8)

* [Change file owner and group - GNU Coreutils](https://www.gnu.org/software/coreutils/manual/html%5Fnode/chown-invocation.html)
* [chown(1) — Linux manual page](https://www.man7.org/linux/man-pages/man1/chown.1.html)

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#5fe4e2)[手册](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md#5fe4e2)

### 显示

```text
CHOWN(1)                         User Commands                        CHOWN(1)

NAME
       chown - change file owner and group

SYNOPSIS
       chown [OPTION]... [OWNER][:[GROUP]] FILE...
       chown [OPTION]... --reference=RFILE FILE...

DESCRIPTION
       This manual page documents the GNU version of chown.  chown changes the
       user  and/or  group  ownership of each given file.  If only an owner (a
       user name or numeric user ID) is given, that user is made the owner  of
       each  given file, and the files' group is not changed.  If the owner is
       followed by a colon and a group name (or numeric  group  ID),  with  no
       spaces  between  them,  the  group ownership of the files is changed as
       well.  If a colon but no group name follows the user name, that user is
       made the owner of the files and the group of the files  is  changed  to
       that  user's  login  group.   If the colon and group are given, but the
       owner is omitted, only the group of the files is changed; in this case,
       chown performs the same function as chgrp.  If only a colon  is  given,
       or  if  the entire operand is empty, neither the owner nor the group is
       changed.

OPTIONS
       Change the owner and/or group of each FILE to OWNER and/or GROUP.  With
       --reference, change the owner and group of each FILE to those of RFILE.

       -c, --changes
              like verbose but report only when a change is made

       -f, --silent, --quiet
              suppress most error messages

       -v, --verbose
              output a diagnostic for every file processed

       --dereference
              affect the referent of each symbolic link (this is the default),
              rather than the symbolic link itself

       -h, --no-dereference
              affect symbolic links instead of  any  referenced  file  (useful
              only on systems that can change the ownership of a symlink)

       --from=CURRENT_OWNER:CURRENT_GROUP
              change  the  owner and/or group of each file only if its current
              owner and/or group match those specified here.   Either  may  be
              omitted,  in  which case a match is not required for the omitted
              attribute

       --no-preserve-root
              do not treat '/' specially (the default)

       --preserve-root
              fail to operate recursively on '/'

       --reference=RFILE
              use RFILE's owner and group rather than  specifying  OWNER:GROUP
              values.  RFILE is always dereferenced.

       -R, --recursive
              operate on files and directories recursively

       The  following  options modify how a hierarchy is traversed when the -R
       option is also specified.  If more than one is specified, only the  fi‐
       nal one takes effect.

       -H     if  a  command  line argument is a symbolic link to a directory,
              traverse it

       -L     traverse every symbolic link to a directory encountered

       -P     do not traverse any symbolic links (default)

       --help display this help and exit

       --version
              output version information and exit

       Owner is unchanged if missing.  Group  is  unchanged  if  missing,  but
       changed  to login group if implied by a ':' following a symbolic OWNER.
       OWNER and GROUP may be numeric as well as symbolic.

EXAMPLES
       chown root /u
              Change the owner of /u to "root".

       chown root:staff /u
              Likewise, but also change its group to "staff".

       chown -hR root /u
              Change the owner of /u and subfiles to "root".

AUTHOR
       Written by David MacKenzie and Jim Meyering.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright © 2023 Free Software Foundation, Inc.   License  GPLv3+:  GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       chown(2)

       Full documentation <https://www.gnu.org/software/coreutils/chown>
       or available locally via: info '(coreutils) chown invocation'

GNU coreutils 9.4                 April 2024                          CHOWN(1)

```

---

> 《[Bash 的 chown 命令](https://xplanc.online/055f1d19fa8e22c401338a248207139082885ec8c038e593131e2312ff8f3ae1)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chown.md)。