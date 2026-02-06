---
title: Bash 的 grep 命令
tags: [linux,bash,grep]
date: 2026-01-17 16:26:08
---

# grep 命令详解

## 基本概念
[`grep`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.grep.md) (Global Regular Expression Print) 是 Linux/Unix 系统中强大的文本搜索工具，它使用正则表达式在文件中搜索指定模式，并将匹配的行打印出来。grep 由 Ken Thompson 在 1974 年开发，是 Unix 系统中最早的工具之一。

## 基本语法
```
grep [选项] 模式 [文件...]
```

## 常用选项
1. **-i** (ignore-case)：忽略大小写差异
   ```
   grep -i "error" logfile.txt
   ```

2. **-v** (invert-match)：反向匹配，显示不包含模式的行
   ```
   grep -v "success" results.log
   ```

3. **-n** (line-number)：显示匹配行的行号
   ```
   grep -n "warning" system.log
   ```

4. **-c** (count)：统计匹配行数而非显示内容
   ```
   grep -c "404" access.log
   ```

5. **-r** 或 **-R** (recursive)：递归搜索目录中的文件
   ```
   grep -r "function" /home/user/projects/
   ```

6. **-l** (files-with-matches)：只显示包含匹配的文件名
   ```
   grep -l "deprecated" *.py
   ```

7. **-w** (word-regexp)：只匹配完整单词
   ```
   grep -w "main" program.c
   ```

8. **-A** (after-context), **-B** (before-context), **-C** (context)：显示匹配行前后的内容
   ```
   grep -A 2 -B 2 "exception" trace.log
   ```

## 高级用法
1. **使用正则表达式**
   ```
   grep "^[A-Z]" file.txt  # 匹配以大写字母开头的行
   grep "[0-9]\{3\}-[0-9]\{4\}" contacts.txt  # 匹配电话号码格式
   ```

2. **结合其他命令**
   ```
   ps aux | grep "nginx"  # 查找nginx进程
   find /var/log -name "*.log" | xargs grep "error"  # 在日志文件中查找错误
   ```

3. **使用颜色高亮**
   ```
   grep --color=auto "important" notes.txt
   ```

4. **搜索多个模式**
   ```
   grep -e "error" -e "warning" system.log
   ```

## 实际应用场景
1. **日志分析**：快速查找特定错误或事件
   ```
   grep "Failed password" /var/log/auth.log
   ```

2. **代码审查**：查找特定函数或变量使用
   ```
   grep -rn "malloc(" src/
   ```

3. **配置文件检查**：验证特定设置
   ```
   grep "^Listen" /etc/apache2/apache2.conf
   ```

4. **数据处理**：提取特定格式的数据
   ```
   grep -o "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}" emails.txt
   ```

## 变种命令
1. **`egrep`** (或 grep -E)：支持扩展正则表达式
2. **`fgrep`** (或 grep -F)：快速搜索固定字符串，不使用正则表达式
3. **`rgrep`**：递归搜索的快捷方式
4. **`zgrep`**：在压缩文件中搜索

## 性能优化
1. 对于大文件，使用 `-m NUM` 限制匹配行数
2. 明确指定文件类型减少搜索范围
3. 在递归搜索时使用 `--include` 和 `--exclude` 过滤文件

## 注意事项
1. 特殊字符需要使用引号括起来
2. 正则表达式中的元字符可能需要转义
3. 默认情况下，grep 区分大小写
4. 在脚本中使用时，注意处理 grep 的退出状态
