---
title: Linux新手实用命令
tags: [linux,bash,命令]
date: 2026-02-13 15:18:43
---

# Linux 新手实用命令指南

## 基本文件操作命令

1. **ls** - 列出目录内容
   - `ls -l` 以长格式显示文件和目录详细信息
   - `ls -a` 显示所有文件(包括隐藏文件)
   - `ls -lh` 以人类可读格式显示文件大小
   - 示例：`ls -lah /home` 查看/home目录下所有文件的详细信息

2. **cd** - 切换目录
   - `cd ~` 返回用户主目录
   - `cd ..` 返回上一级目录
   - `cd -` 返回上一次所在的目录
   - 示例：`cd /var/log` 进入系统日志目录

3. **mkdir** - 创建目录
   - `mkdir new_folder` 创建单个目录
   - `mkdir -p dir1/dir2/dir3` 创建多级目录
   - 示例：`mkdir -p ~/projects/python/webapp` 创建项目目录结构

4. **cp** - 复制文件/目录
   - `cp file1 file2` 复制文件
   - `cp -r dir1 dir2` 递归复制目录
   - 示例：`cp -r /tmp/backup ~/documents` 备份文件到文档目录

5. **mv** - 移动/重命名文件
   - `mv oldname newname` 重命名文件
   - `mv file1 /target/dir` 移动文件到目标目录
   - 示例：`mv ~/downloads/file.txt ~/documents/` 移动下载的文件到文档目录

## 文件查看与编辑

1. **cat** - 查看文件内容
   - `cat file.txt` 显示文件全部内容
   - `cat file1.txt file2.txt > combined.txt` 合并文件
   - 示例：`cat /etc/passwd` 查看系统用户信息

2. **less/more** - 分页查看文件
   - `less large_file.log` 可上下翻页查看大文件
   - `/keyword` 在less中搜索关键字
   - 示例：`less /var/log/syslog` 查看系统日志

3. **head/tail** - 查看文件开头/结尾
   - `head -n 10 file.txt` 查看文件前10行
   - `tail -f /var/log/app.log` 实时跟踪日志文件变化
   - 示例：`tail -n 20 /var/log/auth.log` 查看最近的20条认证日志

4. **nano** - 简单文本编辑器
   - `nano file.txt` 编辑文件
   - 快捷键：Ctrl+O保存，Ctrl+X退出
   - 示例：`nano ~/.bashrc` 编辑用户bash配置文件

## 系统信息与进程管理

1. **top/htop** - 系统监控
   - `top` 显示系统进程和资源使用情况
   - `htop` (需安装)更友好的交互式进程查看器
   - 示例：在top中按"M"按内存使用排序，按"P"按CPU使用排序

2. **ps** - 查看进程
   - `ps aux` 查看所有运行中的进程
   - `ps -ef | grep nginx` 查找特定进程
   - 示例：`ps aux --sort=-%cpu | head` 查看CPU占用最高的进程

3. **kill** - 终止进程
   - `kill -9 PID` 强制终止指定PID的进程
   - `pkill process_name` 通过进程名终止
   - 示例：`pkill -f "python script.py"` 终止运行的Python脚本

4. **df/du** - 磁盘空间检查
   - `df -h` 查看磁盘使用情况(人类可读格式)
   - `du -sh *` 查看当前目录各文件/目录大小
   - 示例：`du -sh /var/* | sort -h` 查看/var下各目录大小并排序

## 网络相关命令

1. **ping** - 测试网络连接
   - `ping google.com` 测试与Google的连接
   - `ping -c 4 8.8.8.8` 发送4个ping包到Google DNS
   - 示例：`ping -i 5 example.com` 每5秒发送一次ping测试

2. **ifconfig/ip** - 网络接口配置
   - `ifconfig` 查看网络接口信息(旧版)
   - `ip a` 新版查看IP地址和网络接口
   - 示例：`ip route show` 查看路由表

3. **netstat/ss** - 网络连接查看
   - `netstat -tulnp` 查看监听端口和连接(旧版)
   - `ss -tulnp` 新版查看网络连接信息
   - 示例：`ss -tulnp | grep 80` 检查80端口是否被监听

4. **wget/curl** - 下载工具
   - `wget http://example.com/file.zip` 下载文件
   - `curl -O http://example.com/file.zip` 另一种下载方式
   - 示例：`curl -I http://example.com` 仅获取HTTP头信息

## 权限管理

1. **chmod** - 修改文件权限
   - `chmod 755 script.sh` 设置可执行权限
   - `chmod +x file.sh` 添加执行权限
   - 示例：`chmod -R 644 /var/www/html` 递归设置目录权限

2. **chown** - 修改文件所有者
   - `chown user:group file.txt` 修改所有者和组
   - `chown -R www-data:www-data /var/www` 递归修改网站目录所有者
   - 示例：`chown bob:developers project/` 将项目目录所有者改为bob，组改为developers

3. **sudo** - 以超级用户权限执行
   - `sudo command` 以root权限执行命令
   - `sudo -i` 切换到root用户
   - 示例：`sudo apt update` 更新软件包列表(需要root权限)

## 软件包管理

1. **apt** (Debian/Ubuntu)
   - `sudo apt update` 更新软件包列表
   - `sudo apt install package` 安装软件包
   - `sudo apt remove package` 移除软件包
   - 示例：`sudo apt install nginx` 安装Nginx web服务器

2. **yum/dnf** (RHEL/CentOS/Fedora)
   - `sudo yum install package` 安装软件包
   - `sudo dnf remove package` 移除软件包(新版)
   - 示例：`sudo yum install httpd` 安装Apache web服务器

3. **snap** (跨发行版)
   - `sudo snap install package` 安装snap软件包
   - `snap list` 查看已安装的snap包
   - 示例：`sudo snap install code --classic` 安装VS Code

## 搜索与查找

1. **find** - 查找文件
   - `find / -name "*.log"` 在全系统查找.log文件
   - `find ~ -type f -size +10M` 在主目录查找大于10MB的文件
   - 示例：`find /etc -name "*conf*"` 在/etc下查找包含"conf"的文件

2. **grep** - 文本搜索
   - `grep "error" /var/log/syslog` 在日志中搜索"error"
   - `grep -r "function_name" /path/to/code` 递归搜索代码中的函数
   - 示例：`grep -i "warning" *.log` 在当前目录.log文件中不区分大小写搜索"warning"

3. **locate** - 快速文件查找
   - `locate filename` 快速查找文件位置
   - `sudo updatedb` 更新locate数据库
   - 示例：`locate .bashrc` 查找所有.bashrc文件位置

## 压缩与归档

1. **tar** - 打包和解包
   - `tar -cvzf archive.tar.gz dir/` 创建gzip压缩包
   - `tar -xvzf archive.tar.gz` 解压gzip包
   - 示例：`tar -cvjf backup.tar.bz2 /home/user/documents` 创建bzip2压缩包

2. **zip/unzip**
   - `zip archive.zip file1 file2` 创建zip压缩包
   - `unzip archive.zip` 解压zip文件
   - 示例：`zip -r website.zip public_html/` 递归压缩网站目录

3. **gzip/gunzip**
   - `gzip file.txt` 压缩文件(生成file.txt.gz)
   - `gunzip file.txt.gz` 解压文件
   - 示例：`gzip -9 large_file.log` 使用最高压缩率压缩日志文件

## 实用技巧

1. **命令历史**
   - `history` 查看命令历史
   - `!number` 执行历史记录中编号为number的命令
   - `Ctrl+R` 反向搜索命令历史

2. **管道和重定向**
   - `command1 | command2` 将一个命令的输出作为另一个命令的输入
   - `command > file.txt` 将输出重定向到文件
   - `command >> file.txt` 将输出追加到文件
   - 示例：`ls -l /etc | grep network > network_files.txt` 查找/etc下的网络相关文件并保存

3. **别名**
   - `alias ll='ls -lah'` 创建别名
   - `unalias ll` 删除别名
   - 示例：`alias update='sudo apt update && sudo apt upgrade -y'` 创建一键更新别名

4. **帮助手册**
   - `man command` 查看命令手册
   - `command --help` 快速查看命令帮助
   - 示例：`man grep` 查看grep的完整用法