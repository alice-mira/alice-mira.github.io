---
title: Bash 的 sed 命令
tags: [linux,bash,sed]
date: 2026-01-17 16:33:23
---

# sed 命令详解

## 基本概念

[`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md)（Stream EDitor）是一种流编辑器，用于对输入流（文件或管道）进行基本的文本转换。它是 Unix/Linux 系统中的重要工具，通常用于：
- 自动编辑文件
- 简化对多个文件的重复编辑
- 编写转换程序

## 基本语法

```bash
sed [选项] '命令' 输入文件
```

常用选项：
- `-n`：禁止自动打印模式空间
- `-e`：允许多个编辑命令
- `-f`：从文件中读取 sed 脚本
- [`-i`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md)：直接修改文件内容（危险但常用）
- `-r`：使用扩展正则表达式

## 常用命令

### 替换命令

```bash
sed 's/原字符串/新字符串/[标志]' 文件名
```

标志说明：
- `g`：全局替换（默认只替换每行第一个匹配）
- [`p`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.p.md)：打印替换的行
- [`i`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md)：忽略大小写
- `数字`：替换第 N 个匹配

示例：
```bash
# 替换文件中的 "apple" 为 "orange"
sed 's/apple/orange/g' fruits.txt

# 只替换每行第二个 "apple"
sed 's/apple/orange/2' fruits.txt

# 替换并保存修改到原文件
sed -i 's/apple/orange/g' fruits.txt
```

### 删除命令

```bash
# 删除第3行
sed '3d' file.txt

# 删除最后一行
sed '$d' file.txt

# 删除匹配 "pattern" 的行
sed '/pattern/d' file.txt

# 删除从第5行到第10行
sed '5,10d' file.txt
```

### 打印命令

```bash
# 打印第5行
sed -n '5p' file.txt

# 打印从第3行到第7行
sed -n '3,7p' file.txt

# 打印匹配 "error" 的行
sed -n '/error/p' log.txt
```

### 插入和追加

```bash
# 在第3行前插入内容
sed '3i\插入的内容' file.txt

# 在第3行后追加内容
sed '3a\追加的内容' file.txt
```

### 其他常用操作

```bash
# 替换时保留部分原内容（使用 & 符号）
sed 's/[0-9]/数字&/g' file.txt

# 使用分组替换
sed 's/\([a-z]\)\([A-Z]\)/\2\1/' file.txt

# 执行多个命令（用分号分隔）
sed -e 's/foo/bar/g' -e 's/baz/qux/g' file.txt
```

## 高级用法

### 使用正则表达式

```bash
# 替换所有数字为 #
sed 's/[0-9]/#/g' file.txt

# 替换以a开头的单词
sed 's/\<a\w*/REPLACED/g' file.txt

# 删除空行
sed '/^$/d' file.txt
```

### 使用保持空间

保持空间（hold space）是 [`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md) 的另一个缓冲区，可以用来临时存储内容：
```bash
# 交换模式和保持空间内容
sed '1!G;h;$!d' file.txt  # 反转文件行顺序
```

### 分支和标签

```bash
# 跳过某些行的处理
sed '/pattern/{n;d}' file.txt  # 删除匹配行后的下一行

# 使用标签实现循环
sed ':a;s/foo/bar/;ta' file.txt  # 重复替换直到没有更多匹配
```

## 实际应用示例

1. 批量重命名文件：
```bash
ls *.txt | sed 's/\(.*\)\.txt/mv & \1.bak/' | sh
```

2. 提取日志中的特定信息：
```bash
cat server.log | sed -n '/ERROR/,/DEBUG/p'
```

3. 转换文件格式：
```bash
sed 's/^/    /' input.txt > indented.txt  # 添加缩进
```

4. 处理 CSV 文件：
```bash
sed 's/,/ /g' data.csv  # 将逗号替换为空格
```

## 注意事项

1. 使用 [`-i`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md) 选项前最好先测试命令
2. 复杂操作建议先写入脚本文件（使用 `-f` 选项）
3. 对于大文件处理，[`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md) 比大多数编辑器更高效
4. macOS 上的 [`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md) 与 GNU [`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md) 有些语法差异

[`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md) 是一个强大的文本处理工具，熟练掌握可以极大提高文本处理效率。
