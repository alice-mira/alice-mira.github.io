---
title: Bash 的 awk 命令
tags: [linux,bash,awk]
date: 2026-01-17 17:42:51
---

# AWK 命令详解

## 基本概念
[`awk`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.awk.md) 是一种强大的文本处理工具和编程语言，由 Alfred Aho、Peter Weinberger 和 Brian Kernighan 在 1977 年开发（名字取自三人姓氏首字母）。它专门设计用于处理结构化文本数据，如日志文件、CSV 文件等。

## 基本语法

[`awk 'pattern {action}' input_file`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.awk.md)

## 核心组成部分
1. **模式(Pattern)**
   - 正则表达式：`/error/`
   - 关系表达式：`$3 > 100`
   - 特殊模式：
     - `BEGIN`：处理前执行
     - `END`：处理后执行

2. **动作(Action)**
   - 打印语句：`{print $1}`
   - 计算操作：[`{sum += $3}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sum.md)
   - 流程控制：`if-else`, `while`等

## 常用内置变量
- `NR`：当前记录号（行号）
- `NF`：当前记录的字段数
- `FS`：字段分隔符（默认空格）
- `OFS`：输出字段分隔符
- `RS`：记录分隔符（默认换行符）

## 实用示例
1. 打印特定列
```bash
awk '{print $1,$3}' data.txt  # 打印第1和第3列
```

2. 条件过滤
```bash
awk '$3 > 100 {print $0}' data.txt  # 打印第3列大于100的行
```

3. 计算统计
```bash
awk '{sum += $1} END {print sum}' numbers.txt  # 计算第一列总和
```

4. 字段处理
```bash
awk -F',' '{print $2}' csvfile.csv  # 指定逗号为分隔符
```

5. 复杂处理
```bash
awk 'BEGIN {FS=":"; OFS="--"} NR>5 {print $1,$NF}' /etc/passwd
```

## 高级功能
1. 数组处理
```bash
awk '{count[$1]++} END {for (item in count) print item,count[item]}' log.txt
```

2. 自定义函数
```bash
awk 'function myfunc(x) {return x*2} {print myfunc($1)}' data.txt
```

3. 多文件处理
```bash
awk 'FNR==1 {print FILENAME} {print $0}' file1.txt file2.txt
```

## 应用场景
1. 日志分析：提取特定错误信息
2. 数据报表：生成统计摘要
3. 文本转换：格式重组
4. 系统管理：处理配置文件
5. 数据清洗：预处理CSV文件

## 性能提示
1. 对于大文件，考虑使用`mawk`（更快的AWK实现）
2. 复杂操作可考虑结合[`sed`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.sed.md)等其他工具
3. 需要多次处理同一文件时，可先将结果存入变量
```bash
awk '{a[$1]=$2} END {for(i in a) print i,a[i]}' largefile.txt
```

## 版本差异
- `GNU AWK (gawk)`：功能最丰富的实现
- `BWK AWK`：经典实现
- `mawk`：注重性能的实现
```bash
awk --version  # 查看版本信息
```

## 学习资源
1. 官方文档：[`man awk`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.man.md)
2. 经典书籍：《The AWK Programming Language》
3. 在线教程：GNU AWK用户指

