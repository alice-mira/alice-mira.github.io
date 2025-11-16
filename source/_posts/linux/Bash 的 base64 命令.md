---
title: Bash 的 base64 命令
tags: [linux,bash,cd]
date: 2025-11-14 02:14:08
---

# [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#5e77f8)[Bash 的 base64 命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#5e77f8)

```text
base64 [OPTION]... [FILE]...

```

功能

进行 BASE64 编码或解码。

类型

可执行文件（[`/usr/bin/base64`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md)），属于 [coreutils](https://www.gnu.org/software/coreutils/)。

参数

* `OPTION` 选项：  
   * `-d`, `--decode` \- 解码；不带此选项则为编码  
   * [`-i`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md), `--ignore-garbage` \- 解码时忽略无效字符  
   * `-w`, `--wrap=COLS` \- 编码输出时一行的字符数；默认为 76，设为 0 则不换行  
   * `--help` \- 显示帮助  
   * `--version` \- 显示版本
* `FILE` \- 文件列表

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#0d53f0)[示例](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#0d53f0)

```shell
$ man base64 > 1.txt
$ cat 1.txt
BASE64(1)                        User Commands                       BASE64(1)

NAME
       base64 - base64 encode/decode data and print to standard output

SYNOPSIS
       base64 [OPTION]... [FILE]
...
$ base64 1.txt > 2.txt      # 编码
$ cat 2.txt
QkFTRTY0KDEpICAgICAgICAgICAgICAgICAgICAgICAgVXNlciBDb21tYW5kcyAgICAgICAgICAg
ICAgICAgICAgICAgQkFTRTY0KDEpCgpOQU1FCiAgICAgICBiYXNlNjQgLSBiYXNlNjQgZW5jb2Rl
L2RlY29kZSBkYXRhIGFuZCBwcmludCB0byBzdGFuZGFyZCBvdXRwdXQKClNZTk9QU0lTCiAgICAg
ICBiYXNlNjQgW09QVElPTl0uLi4gW0ZJTEVdCgpERVNDUklQVElPTgogICAgICAgQmFzZTY0IGVu
...
$ base64 -d 2.txt           # 解码
BASE64(1)                        User Commands                       BASE64(1)

NAME
       base64 - base64 encode/decode data and print to standard output

SYNOPSIS
       base64 [OPTION]... [FILE]
...

```

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#f837e2)[相关命令](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#f837e2)

| 命令                                                                                                            | 说明                                  |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| [base32](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base32.md) | 进行 BASE32 编码或解码                     |
| [basenc](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.basenc.md) | 进行 BASE2 BASE16 BASE32 BASE64 编码或解码 |

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#fac4c8)[推荐阅读](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#fac4c8)

* [Transform data into printable data - GNU Coreutils](https://www.gnu.org/software/coreutils/manual/html%5Fnode/base64-invocation.html)
* [base64(1) — Linux manual page](https://www.man7.org/linux/man-pages/man1/base64.1.html)

## [#](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#5fe4e2)[手册](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md#5fe4e2)

### 显示

```text
BASE64(1)                        User Commands                       BASE64(1)

NAME
       base64 - base64 encode/decode data and print to standard output

SYNOPSIS
       base64 [OPTION]... [FILE]

DESCRIPTION
       Base64 encode or decode FILE, or standard input, to standard output.

       With no FILE, or when FILE is -, read standard input.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.

       -d, --decode
              decode data

       -i, --ignore-garbage
              when decoding, ignore non-alphabet characters

       -w, --wrap=COLS
              wrap encoded lines after COLS character (default 76).  Use 0  to
              disable line wrapping

       --help display this help and exit

       --version
              output version information and exit

       The  data are encoded as described for the base64 alphabet in RFC 4648.
       When decoding, the input may contain newlines in addition to the  bytes
       of  the formal base64 alphabet.  Use --ignore-garbage to attempt to re‐
       cover from any other non-alphabet bytes in the encoded stream.

AUTHOR
       Written by Simon Josefsson.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright © 2023 Free Software Foundation, Inc.   License  GPLv3+:  GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       basenc(1)

       Full documentation <https://www.gnu.org/software/coreutils/base64>
       or available locally via: info '(coreutils) base64 invocation'

GNU coreutils 9.4                 April 2024                         BASE64(1)

```

---

> 《[Bash 的 base64 命令](https://xplanc.online/e8535ed007b2e08136d08d781b455bbac586676babdcd97d17c1f804458928c5)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.base64.md)。