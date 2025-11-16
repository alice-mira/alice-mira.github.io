---
title: Bash 入门
tags: [linux,bash,cd]
date: 2025-11-15 23:32:16
---

# [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#dff7f4)[Bash 入门](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#dff7f4)

## [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#a591a6)[Hello World](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#a591a6)

Bash 的内置命令 [echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 可以打印文本。例如：

```shell
$ echo Hello World
Hello World

```

[echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 命令的 `-e` 选项激活转义字符的解释。例如：

```shell
$ echo -e "Hello \n World"
Hello 
 World

```

## [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#0953d7)[命令格式](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#0953d7)

Bash 命令基本遵循以下格式：

```text
命令 参数1 参数2 参数3 ...

```

例如在 [`echo Hello World`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 中，[echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 是命令，`Hello` 是参数1，`World` 是参数2。

而在 [`echo -e "Hello \n World"`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 中，[echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 是命令，`-e` 是参数1，`"Hello \n World"` 是参数2。

## [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#508bf3)[注释](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#508bf3)

注释（comment）是写在程序里的**说明性文字**，不会被执行。

Bash 中的注释使用 `#` 表示，例如：

```shell
$ # 这是注释，不会执行
$ echo Hello World # 这也是注释
Hello World

```

* 只会打印 `Hello World` 不会打印 `# 这也是注释`

如果要让 `#` 表示该字符本身（而不是注释），可以使用 `\` 转义或者使用引号包裹。

例如：

```shell
$ \# 这不是注释，会执行
bash: #: No such file or directory
$ echo Hello World \# 这不是注释
Hello World # 这不是注释
$ echo "Hello World # 这也不是注释"
Hello World # 这也不是注释

```

# [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#6acab8)[#!Shebang](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#6acab8)

`#!`（读作 shebang）是 Bash 中的一个特殊标记，写在脚本文件的开头，用来表示该文怎样运行。

例如：

demo.sh

```bash
#!/usr/bin/bash
echo Hello World

```

* [`#!/usr/bin/bash`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md) 表示通过 [`/usr/bin/bash demo.sh`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md) 命令解释执行

demo.py

```python
#!/usr/bin/env pyhon3
print("hello world")

```

* [`#!/usr/bin/env pyhon3`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md) 表示通过 [`/usr/bin/env pyhon3 demo.py`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md) 命令解释执行

## [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#f64bb8)[命令类型](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#f64bb8)

Bash 中的命令主要分为四类：

1. 内置命令
2. 可执行程序（外部命令）
3. 函数
4. 别名

可以通过 [type](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.type.md) 查看命令的类型。例如：

```shell
$ type type 
type is a shell builtin
$ type echo
echo is a shell builtin
$ type ls
ls is aliased to 'ls --color=auto'
$ type cat
cat is /usr/bin/cat

```

* [type](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.type.md) 本身是一个内置命令
* [echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md) 是内置命令
* [ls](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.ls.md) 是 [`ls --color=auto`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.ls.md) 的别名
* [cat](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cat.md) 是可执行程序，路径为 [`/usr/bin/cat`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md)

### [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#55c4cb)[别名](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#55c4cb)

[`alias`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.alias.md) 命令可以查看和定义别名，[`unalias`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.unalias.md) 命令可以删除别名。格式为：

```bash
alias               # 查看所有别名
alias 别名          # 查看指定别名
alias 别名='命令'   # 定义别名
unalias             # 删除别名

```

例如：

```shell
$ alias greet='echo Hello'      # 定义别名
$ alias greet                   # 查看别名
alias greet='echo Hello'
$ greet                         # 执行别名
Hello
$ unalias greet                 # 删除别名
$ alias greet                   # 查看别名
-bash: alias: greet: not found

```

在命令前加上反斜杠（`\`）可以抑制别名。例如：

```shell
$ type -a ls                    # 查看所有可用的 ls 命令
ls is aliased to `ls --color=auto'
ls is /usr/bin/ls
ls is /bin/ls
$ ls                            # 实际执行 ls --color=auto
1.txt 2.txt dir1 dir2
$ \ls                           # 实际执行 /usr/bin/ls
1.txt 2.txt dir1 dir2

```


### [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#0ad2a1)[基础命令](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#0ad2a1)

| 命令                                                                                                                                                                                                                    | 说明          | 示例                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------- |
| [echo](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.echo.md)                                                                                                             | 输出文字或变量值    | echo "Hello Bash" echo $HOME                                                                                         |
| [pwd](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.pwd.md)                                                                                                               | 显示当前工作目录路径  | [pwd](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.pwd.md) → /home/user |
| [ls](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.ls.md)                                                                                                                 | 列出目录内容      | ls -l（详细格式） ls -a（显示隐藏文件）                                                                                            |
| [cd](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md)                                                                                                                 | 切换工作目录      | cd /etc（进入 /etc） cd ..（返回上一级）                                                                                        |
| [mkdir](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.mkdir.md)                                                                                                           | 创建目录        | mkdir new\_folder                                                                                                    |
| [rmdir](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.rmdir.md)                                                                                                           | 删除空目录       | rmdir old\_folder                                                                                                    |
| [cp](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cp.md)                                                                                                                 | 复制文件或目录     | cp file1.txt file2.txt cp -r dir1 dir2（递归复制目录）                                                                       |
| [mv](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.mv.md)                                                                                                                 | 移动或重命名文件    | mv old.txt new.txt（重命名） mv file.txt /tmp/（移动）                                                                        |
| [rm](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.rm.md)                                                                                                                 | 删除文件或目录     | rm file.txt rm -D dir/（删除空目录） rm -r dir/（递归删除目录） rm -rf \*（强制删除全部）                                                   |
| [touch](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.touch.md)                                                                                                           | 创建空文件或更新时间戳 | touch new.txt                                                                                                        |
| [cat](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cat.md)                                                                                                               | 查看文件内容      | cat file.txt                                                                                                         |
| [more](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.more.md) / [less](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.less.md) | 分页查看文件      | less large.txt（可上下翻页）                                                                                                |
| [head](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.head.md)                                                                                                             | 查看文件前几行     | head -n 10 file.txt                                                                                                  |
| [tail](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.tail.md)                                                                                                             | 查看文件末几行     | tail -n 20 file.txt tail -f log.txt（实时查看）                                                                            |

### [#](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#c36ef5)[常用快捷键](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md#c36ef5)

* `Ctrl + C` \- 中断程序的运行
* `Ctrl + Z` \- 暂停程序的运行，可以通过 `fg` 命令恢复运行
* `Ctrl + D` \- 退出 Bash
* `Ctrl + A` \- 光标移动到行首
* `Ctrl + E` \- 光标移动到行尾
* `Ctrl + U` \- 删除从光标位置到行首的内容
* `Ctrl + K` \- 删除从光标位置到行尾的内容
* `Shift + PageUp` \- 向上翻页
* `Shift + PageDown` \- 向下翻页

---

> 《[Bash 入门](https://xplanc.online/11f30813d56b224b487ae4c84eadf1713ed0febdda20a66a4c438ecc50499a03)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/10.Bash/01.%E5%9F%BA%E7%A1%80/01.%E5%BC%80%E5%A7%8B.md)。