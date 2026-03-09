---
title: Linux的chmod命令
tags: [linux,bash,权限]
date: 2026-03-07 08:08:08
---

Linux 的 [`chmod`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md) 命令是一个用于修改文件或目录权限的重要工具。以下是关于 [`chmod`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md) 命令的详细说明：

1. 基本语法
```
chmod [选项] 模式 文件/目录
```
3. 权限表示方法
有两种主要表示方式：
- 符号模式（字母表示）
  u：用户(owner)
  g：组(group)
  o：其他用户(other)
  a：所有用户(all)
  
  操作符：
  +：添加权限
  -：移除权限
  =：设置权限
  
  权限类型：
  r：读(4)
  w：写(2)
  x：执行(1)

- 数字模式（八进制表示）
  用3位数字表示权限组合，每位数字是r/w/x的数值和

3. 常用选项
-R：递归修改目录及其内容权限
-v：显示详细修改信息
-f：强制修改，不显示错误信息

4. 使用示例
- 符号模式：
  - [`chmod u+x file.txt    # 给所有者添加执行权限`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
  - [`chmod go-rw file.txt  # 移除组和其他用户的读写权限`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
  - [`chmod a=rw file.txt   # 设置所有用户为读写权限`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)

- 数字模式：
  - [`chmod 755 file.txt    # 所有者rwx，组和其他用户rx`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
  - [`chmod 644 file.txt    # 所有者rw，组和其他用户r`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
  - [`chmod 600 file.txt    # 只有所有者有rw权限`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)

5. 特殊权限
- `setuid(4)`：执行时以所有者身份运行
- `setgid(2)`：执行时以组身份运行
- `sticky bit(1)`：目录中只有文件所有者能删除文件

6. 注意事项
- 修改系统文件权限需谨慎
- 使用-R选项时要小心，避免误操作
- 普通用户只能修改自己拥有的文件权限
- 查看当前权限可用[`ls -l`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.ls.md)命令

7. 实际应用场景
- 使脚本可执行：[`chmod +x script.sh`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
- 保护敏感文件：[`chmod 600 secret.txt`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
- 共享目录设置：[`chmod 1777 /tmp`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)
- 修改web目录权限：[`chmod -R 755 /var/www/html`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.chmod.md)