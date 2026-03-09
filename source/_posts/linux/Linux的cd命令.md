---
title: Linux的cd命令
tags: [linux,bash,命令]
date: 2026-02-14 11:32:58
---

Linux的[`cd`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.cd.md)命令（Change Directory）是用于切换当前工作目录的基本命令。以下是对该命令的详细说明：

### 基本语法
```bash
cd [目录路径]
```

### 常用用法

1. **切换到绝对路径**
```bash
cd /usr/local/bin
```

2. **切换到相对路径**
```bash
cd ../parent_directory  # 切换到上级目录下的parent_directory
cd ./subdirectory      # 切换到当前目录下的subdirectory
```

3. **特殊路径**
```bash
cd ~      # 切换到当前用户的主目录
cd        # 同上，切换到主目录
cd -      # 切换到上一个工作目录
cd ..     # 切换到上级目录
```

### 实用技巧

1. **结合Tab键自动补全**
在输入目录名时，可以按Tab键自动补全目录名称

2. **环境变量使用**
```bash
cd $HOME  # 等同于cd ~
```

3. **查找并切换目录**
```bash
cd $(find / -name "target_dir" -type d 2>/dev/null | head -1)
```

### 注意事项

1. 如果目录路径包含空格或特殊字符，需要用引号括起来：
```bash
cd "dir with spaces"
```

2. 目录不存在时会报错：
```bash
cd non_existent_dir  # 会显示"No such file or directory"
```

3. 权限不足时无法进入目录：
```bash
cd /root  # 普通用户通常会提示"Permission denied"
```

### 实际应用场景

1. **项目开发中快速切换目录**
```bash
cd ~/projects/current_project/src/main/java
```

2. **系统维护时访问日志目录**
```bash
cd /var/log
```

3. **在多级目录间快速跳转**
```bash
cd ../../another/project/dir
```

### 相关命令

- [`pwd`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.pwd.md)：显示当前工作目录
- [`ls`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.ls.md)：列出目录内容
- [`pushd`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.pushd.md)/[`popd`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.popd.md)：目录栈操作命令

掌握cd命令是使用Linux系统的基础，熟练运用可以大大提高工作效率。