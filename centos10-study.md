# 1. 配置

## 1. 配置dns

输入 `sudo nmtui`。

选择 **Edit a connection**。

选中你公司的 WiFi，按回车进入。

找到 **IPv4 CONFIGURATION**，

点击 `<Show>`，在 **DNS servers** 处输入 `223.5.5.5`。

一路点击 `<OK>` 退出。

回到主菜单选择 **Activate a connection**，先禁用再重新启用该 WiFi。



# 2. 命令

| 分类     | 命令                  | 作用               | 示例                      |
| -------- | --------------------- | ------------------ | ------------------------- |
| 系统信息 | `uname -a`            | 查看系统信息       | `uname -a`                |
|          | `cat /etc/os-release` | 查看系统版本       | `cat /etc/os-release`     |
|          | `uptime`              | 查看运行时间和负载 | `uptime`                  |
|          | `date`                | 查看系统时间       | `date`                    |
|          | `cal`                 | 查看日历           | `cal`                     |
| 文件操作 | `ls`                  | 查看目录文件       | `ls -l`                   |
|          | `cd`                  | 切换目录           | `cd /home`                |
|          | `pwd`                 | 当前路径           | `pwd`                     |
|          | `cp`                  | 复制文件           | `cp a.txt b.txt`          |
|          | `mv`                  | 移动/重命名        | `mv a.txt /tmp/`          |
|          | `rm`                  | 删除文件           | `rm -rf dir`              |
|          | `mkdir`               | 创建目录           | `mkdir test`              |
|          | `touch`               | 创建空文件         | `touch a.txt`             |
| 文件查看 | `cat`                 | 查看文件内容       | `cat file.txt`            |
|          | `less`                | 分页查看           | `less file.txt`           |
|          | `more`                | 分页查看           | `more file.txt`           |
|          | `head`                | 查看前几行         | `head -n 10 file.txt`     |
|          | `tail`                | 查看后几行         | `tail -f log.txt`         |
| 搜索     | `find`                | 查找文件           | `find / -name "*.log"`    |
|          | `grep`                | 文本搜索           | `grep "error" log.txt`    |
|          | `which`               | 查找命令路径       | `which java`              |
| 权限     | `chmod`               | 修改权限           | `chmod 755 file.sh`       |
|          | `chown`               | 修改属主           | `chown user:user file`    |
|          | `chgrp`               | 修改组             | `chgrp root file`         |
| 用户管理 | `useradd`             | 添加用户           | `useradd test`            |
|          | `passwd`              | 修改密码           | `passwd test`             |
|          | `userdel`             | 删除用户           | `userdel test`            |
|          | `whoami`              | 当前用户           | `whoami`                  |
| 进程管理 | `ps`                  | 查看进程           | `ps -ef`                  |
|          | `top`                 | 实时进程           | `top`                     |
|          | `kill`                | 杀进程             | `kill -9 1234`            |
|          | `pkill`               | 按名称杀进程       | `pkill java`              |
| 磁盘     | `df -h`               | 查看磁盘空间       | `df -h`                   |
|          | `du -sh`              | 查看目录大小       | `du -sh /data`            |
|          | `lsblk`               | 查看磁盘设备       | `lsblk`                   |
|          | `mount`               | 挂载磁盘           | `mount /dev/sdb1 /mnt`    |
| 网络     | `ip a`                | 查看IP             | `ip a`                    |
|          | `ping`                | 测试连通性         | `ping google.com`         |
|          | `curl`                | 请求接口           | `curl http://example.com` |
|          | `wget`                | 下载文件           | `wget url`                |
|          | `netstat -tulnp`      | 查看端口           | `netstat -tulnp`          |
|          | `ss -lntp`            | 查看端口（新）     | `ss -lntp`                |
| 软件管理 | `yum install`         | 安装软件           | `yum install git`         |
|          | `yum remove`          | 卸载软件           | `yum remove git`          |
|          | `yum update`          | 更新软件           | `yum update`              |
|          | `rpm -qa`             | 查看安装包         | `rpm -qa`                 |
| 服务管理 | `systemctl start`     | 启动服务           | `systemctl start nginx`   |
|          | `systemctl stop`      | 停止服务           | `systemctl stop nginx`    |
|          | `systemctl restart`   | 重启服务           | `systemctl restart nginx` |
|          | `systemctl status`    | 服务状态           | `systemctl status nginx`  |
| 压缩     | `tar -czvf`           | 压缩               | `tar -czvf a.tar.gz dir`  |
|          | `tar -xzvf`           | 解压               | `tar -xzvf a.tar.gz`      |
|          | `zip`                 | 压缩               | `zip a.zip file`          |
|          | `unzip`               | 解压               | `unzip a.zip`             |
| 关机重启 | `reboot`              | 重启               | `reboot`                  |
|          | `shutdown -h now`     | 关机               | `shutdown -h now`         |



# 3. 网络

| 类型   | 示例    | 说明            |
| ------ | ------- | --------------- |
| lo     | lo      | 本地回环        |
| en     | enp3s0  | 有线网卡        |
| wl     | wlp4s0  | 无线网卡        |
| docker | docker0 | Docker 虚拟网卡 |
| virbr  | virbr0  | 虚拟机网卡      |
| tun    | tun0    | VPN             |
| br     | br0     | 网桥            |