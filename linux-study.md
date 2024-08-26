debian:

环境变量文件: /etc/enviroment

useradd 所在 /usr/sbin/useradd



CI/CD: Continuous Integration/Continuous Delivery (or Deployment)

# 1. 一些命令



| <span style="white-space: nowrap">命令 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;&emsp;&emsp;&emsp;</span> | <span style="white-space: nowrap">说明 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;</span> | <span style="white-space: nowrap">例子 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;</span> |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ssh username@ip_address                                      | 连接主机,username是您的用户名，ip_address是您的Linux主机IP地址 |                                                              |
| ps -ef\|grep 进程名                                          | 查看进程                                                     | ps -ef\|grep java                                            |
| tail -f 文件名                                               | 查看文件详情                                                 | tail -f nohup.out                                            |
| nohup java -jar jar包 > nohup.out 2>&1 &                     | jar包 部署命令 , jar包> 后面 有空格, 详见下方命令解释        | nohup java -jar mahua.jar   > nohup.out 2>&1 &               |
| kill -9 进程号                                               | 杀 进程, 不给反应时间的杀                                    |                                                              |
| find (/查找范围) -name 文件名/文件夹名 [-type d]             | 查找文件 [-type d] 指定查找类型为文件夹                      | find home -name nginx<br>find / -name nginx;                 |
| pwd                                                          | 查看当前位置                                                 |                                                              |
| q                                                            | 不保存退出                                                   |                                                              |
| wq                                                           | 保存后退出                                                   |                                                              |
| q!                                                           | 不保存, 强制退出                                             |                                                              |
| w                                                            | 保存, 但不退出vi                                             |                                                              |
| w 文件名                                                     | 另存为另一个文件, 并不退出vi                                 |                                                              |
| su                                                           | switch user                                                  | su root                                                      |
| echo                                                         | 清除文件内容                                                 | echo > 文件名                                                |
| df                                                           | 查看磁盘空间                                                 |                                                              |
| mkfs                                                         | 格式化磁盘                                                   | mkfs /dev/sdb                                                |
| dpkg                                                         | 为 “Debian” 专门开发的套件管理系统，方便软件的安装、更新及移除 | dpkg  -i  \<deb file name>                                   |
| tar                                                          | -C 表示 换个文件夹                                           | tar -zxvf typora.gz -C /home/wg/typora                       |
| rm -f \<文件 目录>                                           | 强力删除, 不要求确认                                         |                                                              |
| rm 文件名                                                    |                                                              |                                                              |
| rmdir 文件夹名                                               |                                                              |                                                              |
| find / -name 文件名                                          | 准确查找文件                                                 |                                                              |
| whereis <文件名或文件夹名>                                   | 查找所有文件                                                 |                                                              |
| cat /etc/issue 或cat /etc/redhat-release                     | Linux查看版本当前操作系统发行版信息                          |                                                              |
| cat /proc/version                                            | Linux查看当前操作系统版本信息                                |                                                              |
| uname -a                                                     | 查看内核/操作系统/CPU信息                                    |                                                              |
| cat /proc/cpuinfo                                            | 查看CPU信息命令                                              |                                                              |
| fdisk -l                                                     | 查看硬盘信息命令                                             |                                                              |
| fdisk                                                        | 查看分区                                                     |                                                              |
| cat /proc/meminfo                                            | 查看内存信息命令                                             |                                                              |
| netstat                                                      | 查端口号                                                     |                                                              |
| netstat -tunlp                                               | 用于显示tcp udp的端口和进程情况, 详见下方命令解释            |                                                              |
| netstat -tunlp\|grep 端口号                                  | 查看端口号的占用进程                                         | netstat -tunlp\|grep 8080                                    |
| firewall-cmd --zone=public  --list-ports                     | 查看已经对外开放的端口                                       |                                                              |
| firewall-cmd --zone=public --add-port=8080/tcp --permanent   | 添加开放对外的端口(8080)                                     |                                                              |
| firewall-cmd --reload                                        | 重新载入一下防火墙设置，使设置生效                           |                                                              |
| firewall-cmd --zone=public --query-port=2228/tcp             | 通过命令查看是否生效                                         |                                                              |
| firewall-cmd --zone= public--remove-port=80/tcp --permanent  | 删除端口配置                                                 |                                                              |
| firewall-cmd --zone=public --add-port=100-500/tcp --permanent | 批量开放100-500之间的端口                                    |                                                              |
| firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.200" port protocol="tcp" port="80" reject" | 限制IP为192.168.0.200的地址禁止访问80端口, 如未生效可编辑文件, vi /etc/firewalld/zones/public.xml |                                                              |
| firewall-cmd --permanent --remove-rich-rule =“xxxx”          | 解除被限制的192.168.0.200 (还不确定, 没实验过)               |                                                              |
| firewall-cmd --zone=public --list-rich-rules                 | 查看 被限制的                                                |                                                              |
| firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="10.0.0.0/24" port protocol="tcp" port="80" reject" | 限制10.0.0.0-10.0.0.255这一整个段的IP，禁止他们访问,其中10.0.0.0/24表示为从10.0.0.0这个IP开始,24代表子网掩码为255.255.255.0,共包含256个地址 |                                                              |
| systemctl restart firewalld.service                          | 重启防火墙                                                   |                                                              |
| date                                                         | 查看系统时间                                                 |                                                              |
| timedatectl list-timezones                                   | centos7 列出所有时区                                         |                                                              |
| timedatectl set-timezone Asia/Shanghai                       | centos7 修改时区为 上海                                      |                                                              |
| ssh usr@ip                                                   | 连其他主机                                                   |                                                              |
| sudo passwd root                                             | 修改root 密码                                                |                                                              |
| mv 原文件名 修改后的文件名                                   | 修改文件名                                                   |                                                              |
| chmod -R 777 文件夹                                          | 给文件夹下所有文件 赋权限                                    |                                                              |
| cp -r /home/packageA/* /home/cp/packageB/                    | 复制文件夹下的所有文件 到另一个文件夹下                      |                                                              |
| unzip zip文件名                                              | 解压zip文件, jar包                                           |                                                              |
| tar -zxvf gz文件名                                           | 解压gz文件                                                   |                                                              |
| unzip 壓縮包名                                               | 解壓zip文件, jar包                                           |                                                              |
| unzip -d 指定目录名 要解压的文件                             | -d 后接目录： 指定文件解压缩后所要存储的目录；               |                                                              |
| ln -s  源文件 目标文件                                       | 为某一个文件在另外一个位置建立一个同不的链接，这个命令最常用的参数是-s |                                                              |
| sudo apt autoremove                                          | 清理系统                                                     |                                                              |
| find . -type d -empty -delete                                | 删除所有空目录                                               |                                                              |
| sudo apt-get -f install                                      | 修复依赖包                                                   |                                                              |
| systemctl disable 服务名                                     | 禁止开机启动服务                                             |                                                              |
| systemctl enable 服务名                                      | 开启开机启动服务                                             |                                                              |
| shutdown -r now [reboot]                                     | 立即重启                                                     |                                                              |
| shutdown -r 20:35 [shutdown -r 10 (10分钟后重启)]            | 在时间为20:35时候重启(root用户使用) 如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启 |                                                              |
| shutdown -h now  [halt, poweroff, init 0]                    | 关机                                                         |                                                              |
| shutdown -h 10                                               | 10分钟后关机                                                 |                                                              |
| reboot[shutdown -r now, init 1]                              | 立刻重启                                                     |                                                              |
| shutdown -r 10                                               | 10分钟后重启, 可以用shutdown -c命令取消重启                  |                                                              |
| shutdown -r 20:35                                            | 在某个时刻重启, 可以用shutdown -c命令取消重启                |                                                              |
| shutdown -c                                                  | 如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消重启 |                                                              |
| tcpdump -nn -i eth0 port 80                                  | 用于网络数据包捕获<br />-nn : 这个选项告诉 tcpdump 不要进行 DNS 反向解析。第一个 `n` 表示以数字形式显示 IP 地址，而不是尝试将其解析为主机名；第二个 `n` 表示端口号也直接以数字形式显示，不转换为服务名称。这样可以加快输出速度并避免因 DNS 查找导致的延迟<br />-i : 指定了要监听的网络接口。在这个例子中，`eth0` 代表第一个以太网接口。如果你的系统有不同的网络接口，这里的 `eth0` 应替换为你实际要监控的接口名称<br />prot 80 : 这是一个过滤条件，表示只捕获目标端口或源端口为 80 的数据包。端口 80 通常是 HTTP 协议的默认端口，因此这个命令会捕获所有进出的 HTTP 流量 |                                                              |
| cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime          | 修改 时区                                                    |                                                              |
| date -s 时间                                                 | 修改时间                                                     | date -s '2000-12-12 12:12:12'                                |
| mv 文件[夹]a  文件[夹]b                                      | 重命名文件夹                                                 |                                                              |
| mysql  -u   用户名  -p  <数据库名>                           | 进入mysql                                                    |                                                              |
| redis-cli ping                                               | 查看redis 连接状态                                           |                                                              |
| timedatectl                                                  | 查看时区                                                     |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |



## node 命令

 

| command |      |      |
| ------- | ---- | ---- |
|         |      |      |
|         |      |      |
|         |      |      |



## tee

用于显示程序的输出, 并将其复制到某个文件中

# 2. 文件夹意义

| 文件夹                  | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| etc                     | 存放配置文件<br>and so on的意思来源于 法语的 et cetera 翻译成中文就是 等等 的意思. 至于为什么在/etc下面存放配置文件， 按照原始的UNIX的说法(linux文件结构参考UNIX的教学实现MINIX) 这下面放的都是一堆零零碎碎的东西, 就叫etc, 这其实是个历史遗留. |
| lib                     | 共享库<br>根文件系统目录下程序和核心模块的共享库，存放了根文件系统程序     运行所需的共享文件。这些文件包含了可被许多程序共享的代码     以避免每个程序都包含有相同的子程序的副本     故可以使得可执行文件变得更小，节省空间。 |
| mnt                     | 这个目录是空的，系统提供这个目录是让用户临时挂载别的文件系统 |
| boot                    | 这里存放的是启动LINUX时使用的一些核心文件，引导加载器(bootstrap loader)如LILO     会使用这些文件，当计算机启动时这些文件首先被装载。这个目录也会包含LINUX核（压缩文件 vmlinuz）     但LINUX核也可以存在别处，只要配置LILO并且LILO知道LINUX核在哪儿。 |
| sbin                    | s就是Super User的意思，/sbin目录类似/bin ，也用于存储二进制文件。     但其中的大部分文件多是系统管理员使用的基本的系统管理程序     所以虽然普通用户必要且允许时可以使用，但一般不给普通用户使用。 |
| root                    | 系统管理员(超级用户或根用户)的主目录                         |
| dev                     | 这个目录下是所有LINUX的外部设备文件，其功能类似DOS下的.sys和Win下的.vxd，用户可以通过这些文件访问外部设备，在LINUX中设备和文件是用同种方法访问的。例如:/dev/hda代表第一个物理IDE硬盘 |
| usr                     | "usr" 是 "User System Resources" 的缩写，意思是 “用户系统资源”。它是一个非常重要的文件夹，包含了许多应用程序和文件，以及一些用于支持系统的文件。此外，“usr”文件夹中的内容通常不会被修改，并且会在操作系统更新时得到保留。 |
| /usr/share/applications | 桌面图标的位置                                               |
| /lib                    | apt 安装的程序 如 jvm mysql  都在这个文件夹下                |
| /opt                    | 主要用于安装可选的应用程序包。这里的“opt”可以理解为“optional”（可选的）。这个目录通常用于存放那些非标准的、由第三方提供的软件包，这些软件包不是系统默认安装的一部分 |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |



# 3. 缩写

| 简写  | 全称                 | 解释                                                         |
| ----- | -------------------- | ------------------------------------------------------------ |
| su    | switch user          | 切换用户<br>使用su的缺点之一在于必须要先告知超级用户的密码   |
| sudo  | switch user do       | sudo使一般用户不需要知道超级用户的密码即可获得权限           |
| pwd   | print work direcory  | 打印工作目录, 显示当前位置                                   |
| ps    | process status       | 进程状态 ,进程信息虚拟文件系统，提供了对进程和内核状态的访问接口。 |
| rm    | remove               | 删除                                                         |
| rmdir | remove directory     | 删除目录                                                     |
| man   | manual               | 手册                                                         |
| ln -s | link -soft           | 创建快捷方式                                                 |
| /usr  | unix shared resource | unix共享资源                                                 |
| /proc | processes            | 进程                                                         |
| etc   | et cetera            | 存放系统中所有主要配置文件，如网络配置、用户账号信息等。     |
| nohup | no hang up           | 不挂断                                                       |
| opt   | optional             | 用于存放可选的第三方应用程序，如 Oracle 数据库、Adobe 软件等。 |
| var   | variable             | 动态数据，包括日志文件、缓存数据、邮件等。                   |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |
|       |                      |                                                              |





# 4. 经验



## 1. apt安装后, 设置 java_home

1. 看下是否被设置到环境变量：

>  echo $JAVA_HOME

*这里使用apt install安装，并没有把JAVA_HOME内置到环境变量，那么我们先看下java安装到哪里了。*

>  which java



1. 查看apt 安装的java 到底在哪

>  update-alternatives --config java



2. 然后设置java_home

> vi /etc/profile



3. 重新加载一下环境变量

> source /etc/profile





目前我的mysql 在 /usr/share/mysql

## 2. linux 部署java项目

不指定配置文件

> java -jar jar包



指定配置文件

> java -jar jar包 --sjpring.config.location=路径/配置文件



指定配置文件并指定日志文件位置

>  nohup java -jar /路径/xxx.jar --spring.sjpring.config.location=路径/配置文件 >/路径/xxx.log &



查看日志

> tail -f 日志文件(xx.log)





springboot 加载配置文件的优先级

工程根目录/config/

工程根目录 /

classpath /config/

classpath /



## 3. nginx 配置详解



user nginx nginx ;

Nginx用户及组：用户 组。window下不指定



worker_processes 8;

工作进程：数目。根据硬件调整，通常等于CPU数量或者2倍于CPU。



pid logs/nginx.pid;

pid（进程标识符）：存放路径。



events

{

use epoll;

使用epoll的I/O 模型。linux建议epoll，FreeBSD建议采用kqueue，window下不指定。



worker_connections 204800;

没个工作进程的最大连接数量。根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。每个进程允许的最多连接数，理论上每台nginx服务器的最大连接数为。worker_processes*worker_connections



keepalive_timeout 60;

keepalive超时时间



client_header_buffer_size 4k;

客户端请求头部的缓冲区大小。这个可以根据你的系统分页大小来设置，一般一个请求头的大小不会超过1k，不过由于一般系统分页都要大于1k，所以这里设置为分页大小。

分页大小可以用命令getconf PAGESIZE 取得。但也有client_header_buffer_size超过4k的情况，但是client_header_buffer_size该值必须设置为“系统分页大小”的整倍数。



open_file_cache max=65535 inactive=60s;

这个将为打开文件指定缓存，默认是没有启用的，max指定缓存数量，建议和打开文件数一致，inactive是指经过多长时间文件没被请求后删除缓存



open_file_cache_valid 80s;

这个是指多长时间检查一次缓存的有效信息。



open_file_cache_min_uses 1;

open_file_cache指令中的inactive参数时间内文件的最少使用次数，如果超过这个数字，文件描述符一直是在缓存中打开的，如上例，如果有一个文件在inactive时间内一次没被使用，它将被移除。

}



\##设定http服务器，利用它的反向代理功能提供负载均衡支持

http

{

include mime.types;

设定mime类型,类型由mime.type文件定义



log_format main '$remote_addr - $remote_user [$time_local] "$request" '

'$status $body_bytes_sent "$http_referer" '

'"$http_user_agent" "$http_x_forwarded_for"';

log_format log404 '$status [$time_local] $remote_addr $host$request_uri $sent_http_location';

日志格式设置。

$remote_addr与$http_x_forwarded_for用以记录客户端的ip地址；

$remote_user：用来记录客户端用户名称；

$time_local： 用来记录访问时间与时区；

$request： 用来记录请求的url与http协议；

$status： 用来记录请求状态；成功是200，

$body_bytes_sent ：记录发送给客户端文件主体内容大小；

$http_referer：用来记录从那个页面链接访问过来的；

$http_user_agent：记录客户浏览器的相关信息；

通常web服务器放在反向代理的后面，这样就不能获取到客户的IP地址了，通过$remote_add拿到的IP地址是反向代理服务器的iP地址。反向代理服务器在转发请求的http头信息中，可以增加x_forwarded_for信息，用以记录原有客户端的IP地址和原来客户端的请求的服务器地址。





access_log logs/host.access.log main;

access_log logs/host.access.404.log log404;

用了log_format指令设置了日志格式之后，需要用access_log指令指定日志文件的存放路径；



server_names_hash_bucket_size 128;

\#保存服务器名字的hash表是由指令server_names_hash_max_size 和server_names_hash_bucket_size所控制的。参数hash bucket size总是等于hash表的大小，并且是一路处理器缓存大小的倍数。在减少了在内存中的存取次数后，使在处理器中加速查找hash表键值成为可能。如果hash bucket size等于一路处理器缓存的大小，那么在查找键的时候，最坏的情况下在内存中查找的次数为2。第一次是确定存储单元的地址，第二次是在存储单元中查找键 值。因此，如果Nginx给出需要增大hash max size 或 hash bucket size的提示，那么首要的是增大前一个参数的大小



client_header_buffer_size 4k;

客户端请求头部的缓冲区大小。这个可以根据你的系统分页大小来设置，一般一个请求的头部大小不会超过1k，不过由于一般系统分页都要大于1k，所以这里设置为分页大小。分页大小可以用命令getconf PAGESIZE取得。



large_client_header_buffers 8 128k;

客户请求头缓冲大小。nginx默认会用client_header_buffer_size这个buffer来读取header值，如果

header过大，它会使用large_client_header_buffers来读取。



open_file_cache max=102400 inactive=20s;

这个指令指定缓存是否启用。
例: open_file_cache max=1000 inactive=20s; 

open_file_cache_valid 30s; 

open_file_cache_min_uses 2; 

open_file_cache_errors on;



open_file_cache_errors
语法:open_file_cache_errors on | off 默认值:open_file_cache_errors off 使用字段:http, server, location 这个指令指定是否在搜索一个文件是记录cache错误.

open_file_cache_min_uses

语法:open_file_cache_min_uses number 默认值:open_file_cache_min_uses 1 使用字段:http, server, location 这个指令指定了在open_file_cache指令无效的参数中一定的时间范围内可以使用的最小文件数,如果使用更大的值,文件描述符在cache中总是打开状态.
open_file_cache_valid

语法:open_file_cache_valid time 默认值:open_file_cache_valid 60 使用字段:http, server, location 这个指令指定了何时需要检查open_file_cache中缓存项目的有效信息.

 

client_max_body_size 300m;

设定通过nginx上传文件的大小

 

sendfile on;

sendfile指令指定 nginx 是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度，降低系统uptime。

 

tcp_nopush on;

此选项允许或禁止使用socke的TCP_CORK的选项，此选项仅在使用sendfile的时候使用

 

proxy_connect_timeout 90; 
后端服务器连接的超时时间_发起握手等候响应超时时间

 

proxy_read_timeout 180;

连接成功后_等候后端服务器响应时间_其实已经进入后端的排队之中等候处理（也可以说是后端服务器处理请求的时间）

 

proxy_send_timeout 180;

后端服务器数据回传时间_就是在规定时间之内后端服务器必须传完所有的数据

 

proxy_buffer_size 256k;

设置从被代理服务器读取的第一部分应答的缓冲区大小，通常情况下这部分应答中包含一个小的应答头，默认情况下这个值的大小为指令proxy_buffers中指定的一个缓冲区的大小，不过可以将其设置为更小

 

proxy_buffers 4 256k;

设置用于读取应答（来自被代理服务器）的缓冲区数目和大小，默认情况也为分页大小，根据操作系统的不同可能是4k或者8k

 

proxy_busy_buffers_size 256k;

 

proxy_temp_file_write_size 256k;

设置在写入proxy_temp_path时数据的大小，预防一个工作进程在传递文件时阻塞太长

 

proxy_temp_path /data0/proxy_temp_dir;

proxy_temp_path和proxy_cache_path指定的路径必须在同一分区

proxy_cache_path /data0/proxy_cache_dir levels=1:2 keys_zone=cache_one:200m inactive=1d max_size=30g;
\#设置内存缓存空间大小为200MB，1天没有被访问的内容自动清除，硬盘缓存空间大小为30GB。

keepalive_timeout 120;

keepalive超时时间。

 

tcp_nodelay on;

 

client_body_buffer_size 512k;
如果把它设置为比较大的数值，例如256k，那么，无论使用firefox还是IE浏览器，来提交任意小于256k的图片，都很正常。如果注释该指令，使用默认的client_body_buffer_size设置，也就是操作系统页面大小的两倍，8k或者16k，问题就出现了。
无论使用firefox4.0还是IE8.0，提交一个比较大，200k左右的图片，都返回500 Internal Server Error错误

 

proxy_intercept_errors on;

表示使nginx阻止HTTP应答代码为400或者更高的应答。

 

upstream bakend {

server 127.0.0.1:8027;

server 127.0.0.1:8028;

server 127.0.0.1:8029;

hash $request_uri;

}

nginx的upstream目前支持4种方式的分配

1、轮询（默认）

每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。

2、weight
指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。
例如：
upstream bakend {
server 192.168.0.14 weight=10;
server 192.168.0.15 weight=10;
}

2、ip_hash
每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。
例如：
upstream bakend {
ip_hash;
server 192.168.0.14:88;
server 192.168.0.15:80;
}

3、fair（第三方）
按后端服务器的响应时间来分配请求，响应时间短的优先分配。
upstream backend {
server server1;
server server2;
fair;
}

4、url_hash（第三方）

按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。

例：在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法

upstream backend {
server squid1:3128;
server squid2:3128;
hash $request_uri;
hash_method crc32;
}

tips:

upstream bakend{#定义负载均衡设备的Ip及设备状态}{
ip_hash;
server 127.0.0.1:9090 down;
server 127.0.0.1:8080 weight=2;
server 127.0.0.1:6060;
server 127.0.0.1:7070 backup;
}
在需要使用负载均衡的server中增加
proxy_pass http://bakend/;

每个设备的状态设置为:
1.down表示单前的server暂时不参与负载
2.weight为weight越大，负载的权重就越大。
3.max_fails：允许请求失败的次数默认为1.当超过最大次数时，返回proxy_next_upstream模块定义的错误
4.fail_timeout:max_fails次失败后，暂停的时间。
5.backup： 其它所有的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻。

nginx支持同时设置多组的负载均衡，用来给不用的server来使用。

client_body_in_file_only设置为On 可以讲client post过来的数据记录到文件中用来做debug
client_body_temp_path设置记录文件的目录 可以设置最多3层目录

location对URL进行匹配.可以进行重定向或者进行新的代理 负载均衡

 

 

\##配置虚拟机

server

{

listen 80;

配置监听端口

 

server_name image.***.com;

配置访问域名

 

location ~* \.(mp3|exe)$ {

对以“mp3或exe”结尾的地址进行负载均衡

 

proxy_pass http://img_relay$request_uri;

设置被代理服务器的端口或套接字，以及URL

 

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

以上三行，目的是将代理服务器收到的用户的信息传到真实服务器上

}

 

location /face {

if ($http_user_agent ~* "xnp") {

rewrite ^(.*)$ http://211.151.188.190:8080/face.jpg redirect;

}

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

error_page 404 502 = @fetch;

}

location @fetch {

access_log /data/logs/face.log log404;

rewrite ^(.*)$ http://211.151.188.190:8080/face.jpg redirect;

}

location /image {

if ($http_user_agent ~* "xnp") {

rewrite ^(.*)$ http://211.151.188.190:8080/face.jpg redirect;

}

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

error_page 404 502 = @fetch;

}

location @fetch {

access_log /data/logs/image.log log404;

rewrite ^(.*)$ http://211.151.188.190:8080/face.jpg redirect;

}

}

 

\##其他举例

server

{

listen 80;

server_name *.***.com *.***.cn;

location ~* \.(mp3|exe)$ {

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

}

location / {

if ($http_user_agent ~* "xnp") {

rewrite ^(.*)$ http://i1.***img.com/help/noimg.gif redirect;

}

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

\#error_page 404 http://i1.***img.com/help/noimg.gif;

error_page 404 502 = @fetch;

}

location @fetch {

access_log /data/logs/baijiaqi.log log404;

rewrite ^(.*)$ http://i1.***img.com/help/noimg.gif redirect;

}

}

server

{

listen 80;

server_name *.***img.com;

 

location ~* \.(mp3|exe)$ {

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

}

location / {

if ($http_user_agent ~* "xnp") {

rewrite ^(.*)$ http://i1.***img.com/help/noimg.gif;

}

proxy_pass http://img_relay$request_uri;

proxy_set_header Host $host;

proxy_set_header X-Real-IP $remote_addr;

proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

\#error_page 404 http://i1.***img.com/help/noimg.gif;

error_page 404 = @fetch;

}

\#access_log off;

location @fetch {

access_log /data/logs/baijiaqi.log log404;

rewrite ^(.*)$ http://i1.***img.com/help/noimg.gif redirect;

}

}

server

{

listen 8080;

server_name ngx-ha.***img.com;

location / {

stub_status on;

access_log off;

}

}

server {

listen 80;

server_name imgsrc1.***.net;

root html;

}

 

server {

listen 80;

server_name ***.com w.***.com;

\# access_log /usr/local/nginx/logs/access_log main;

location / {

rewrite ^(.*)$ http://www.***.com/ ;

}

}

server {

listen 80;

server_name *******.com w.*******.com;

\# access_log /usr/local/nginx/logs/access_log main;

location / {

rewrite ^(.*)$ http://www.*******.com/;

}

}

server {

listen 80;

server_name ******.com;

\# access_log /usr/local/nginx/logs/access_log main;

location / {

rewrite ^(.*)$ http://www.******.com/;

}

}

location /NginxStatus {
stub_status on;
access_log on;
auth_basic "NginxStatus";
auth_basic_user_file conf/htpasswd;
}

\#设定查看Nginx状态的地址

 

location ~ /\.ht {
deny all;
}

\#禁止访问.htxxx文件

}

 

注释：变量

Ngx_http_core_module模块支持内置变量，他们的名字和apache的内置变量是一致的。

首先是说明客户请求title中的行，例如$http_user_agent,$http_cookie等等。

此外还有其它的一些变量

$args此变量与请求行中的参数相等

$content_length等于请求行的“Content_Length”的值。

$content_type等同与请求头部的”Content_Type”的值

$document_root等同于当前请求的root指令指定的值

$document_uri与$uri一样

$host与请求头部中“Host”行指定的值或是request到达的server的名字（没有Host行）一样

$limit_rate允许限制的连接速率

$request_method等同于request的method，通常是“GET”或“POST”

$remote_addr客户端ip

$remote_port客户端port

$remote_user等同于用户名，由ngx_http_auth_basic_module认证

$request_filename当前请求的文件的路径名，由root或alias和URI request组合而成

$request_body_file

$request_uri含有参数的完整的初始URI

$query_string与$args一样

$sheeme http模式（http,https）尽在要求是评估例如

Rewrite ^(.+)$ $sheme://example.com$; Redirect;

$server_protocol等同于request的协议，使用“HTTP/或“HTTP/

$server_addr request到达的server的ip，一般获得此变量的值的目的是进行系统调用。为了避免系统调用，有必要在listen指令中指明ip，并使用bind参数。

$server_name请求到达的服务器名

$server_port请求到达的服务器的端口号

$uri等同于当前request中的URI，可不同于初始值，例如内部重定向时或使用index



## 4. vi 后 查找功能

格式:  "/查找内容" 



## ⑤ centos7 redis 安装

安装gcc依赖

 **yum install -y gcc** 

下载并解压安装包

**wget http://download.redis.io/releases/redis-5.0.3.tar.gz**

**tar -zxvf redis-5.0.3.tar.gz**

cd切换到redis解压目录下，执行编译

**cd redis-5.0.3**

 **make**

安装并指定安装目录

**make install PREFIX=/usr/local/redis**

从 redis 的源码目录中复制 redis.conf 到 redis 的安装目录

 **cp /usr/local/redis-5.0.3/redis.conf /usr/local/redis/bin/**

修改 redis.conf 文件，把 daemonize no 改为 daemonize yes

**vi redis.conf**

后台启动

**./redis-server redis.conf**



设置开机启动

**vi /etc/systemd/system/redis.service**

复制粘贴以下内容：

```xml
[Unit]
Description=redis-server
After=network.target
[Service]
Type=forking
ExecStart=/usr/local/redis/bin/redis-server /usr/local/redis/bin/redis.conf
PrivateTmp=true
[Install]
WantedBy=multi-user.target
```

注意：ExecStart配置成自己的路径 

设置开机启动

**systemctl daemon-reload**

**systemctl start redis.service**

**systemctl enable redis.service**



服务操作命令

systemctl start redis.service  #启动redis服务

systemctl stop redis.service  #停止redis服务

systemctl restart redis.service  #重新启动服务

systemctl status redis.service  #查看服务当前状态

systemctl enable redis.service  #设置开机自启动

systemctl disable redis.service  #停止开机自启动



# 5. 命令解释

## 1. java 程序启动命令

1. ```shell
    nohup java -jar tientsineye.jar > tientsineye.out 2>&1 &
   ```

   

2. ```shell
   nohup java -jar *.jar --spring.config.location=config/application.properties >*.log&
   ```

| command                                   | describle                                                    |
| ----------------------------------------- | ------------------------------------------------------------ |
| nohup                                     | 守护进程 "no hung up": 没有挂断                              |
| java -Duser.timezone=GMT+8  -jar *.jar    | jar包启动, 使用 东八区区时, centos7 有这个问题, java 程序获取的时间 不对应 |
| --spring.config.location=配置文件(带路径) | 指定jar包读取的外部的配置文件                                |
| \>*.log                                   | 日志输出位置                                                 |
| 2>&1                                      | 2>&1是将标准错误（2）重定向到标准输出（&1），标准输出（&1）再被重定向输入到*.log文件中。 |
| &                                         | 守护进程(仅当前连接linux终端用户在线时，一旦该用户断开连接，项目将自动停止，因此需要使用nohup) |



2. netstat -tunlp

- -t (tcp) 仅显示tcp相关选项
- -u (udp)仅显示udp相关选项
- -n 拒绝显示别名，能显示数字的全部转化为数字
- -l 仅列出在Listen(监听)的服务状态
- -p 显示建立相关链接的程序名



## 2. echo

```
#!/bin/bash
echo "Hello"
echo "World"
exec "$@"
```

```
这是一个 Bash 脚本，包含三个命令行操作：

echo "Hello": 打印出 "Hello" 这个字符串。
echo "World": 打印出 "World" 这个字符串。
exec "$@": 执行传入的命令行参数。
这个脚本的作用是先打印出 "Hello" 和 "World" 这两个字符串，然后执行传入的命令行参数。"$@" 是一个特殊的变量，表示所有的命令行参数，通过 $ 和 @ 组合而成。因此，当你在运行这个脚本时，可以在后面加上任意数量的命令行参数，并且这些参数会被传递到 exec 命令的位置，从而执行相应的命令。
```





## 3. ">>"

这个符号

`>>` 是 Shell 中的追加输出符号，与 `>` 的作用不同，`>` 会将原来的文件内容清空并重新写入新的内容。

```
echo "sdfsd" >> wg.txt
```

这条命令的作用是将字符串 "sdfsd" 追加到文件 wg.txt 的末尾，而不会覆盖已有的内容。`>>` 是 Shell 中的追加输出符号，与 `>` 的作用不同，`>` 会将原来的文件内容清空并重新写入新的内容。

如果 wg.txt 文件不存在，则该命令将自动创建一个新文件，并在其中添加字符串 "sdfsd"。如果 wg.txt 已经存在，则会将字符串追加到文件末尾，而不影响原有的内容。

需要注意的是，如果文件已经被其他进程打开，在进行追加操作时可能会出现并发访问问题。为了避免这种情况，可以使用文件锁或其他同步机制来保证安全性



# 6. centos7 安装 postgresql

1、安装rpm文件（可以到官网核定你的版本情况和路径，如果是11版，下面的都需要调整一下）

```c
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```



2、安装客户端

```c
yum install postgresql10
```



3、安装服务端

```c
yum install postgresql10-server
```



4、初始化

```c
/usr/pgsql-10/bin/postgresql-10-setup initdb
```



5、设置自动启动并且启动postgresql服务

```c
systemctl enable postgresql-10
systemctl start postgresql-10
```





**第二部分：创建用户和数据库**

1、使用postgres用户登录（PostgresSQL安装后会自动创建postgres用户，无密码）

```c
su - postgres
```



2、登录postgresql数据库

密码是 psql



3、创建用户和数据库并授权

```c
create user test_user with password 'abc123';            // 创建用户
create database test_db owner test_user;                 // 创建数据库
grant all privileges on database test_db to test_user;   // 授权
```



4、退出psql（输入 \q 再按回车键即可)





# 7. 防火墙的一些



man firewalld.richlanguage  查看防火墙说明文件



firewall-cmd --zone=public  --list-ports  查看已经对外开放的端口   

firewall-cmd --zone=public --add-port=8080/tcp --permanent  添加开放对外的端口(8080)    

firewall-cmd --reload  重新载入一下防火墙设置，使设置生效    

firewall-cmd --zone=public --query-port=2228/tcp  通过命令查看是否生效    

firewall-cmd --zone= public--remove-port=80/tcp --permanent  删除端口配置    

firewall-cmd --zone=public --add-port=100-500/tcp --permanent  批量开放100-500之间的端口  

firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.200" port protocol="tcp" port="80" reject"  限制IP为192.168.0.200的地址禁止访问80端口, 如未生效可编辑文件, vi /etc/firewalld/zones/public.xml      

解除被限制的192.168.0.200    

firewall-cmd --zone=public --list-rich-rules  查看 被限制的   

firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="10.0.0.0/24" port protocol="tcp" port="80" reject"  限制10.0.0.0-10.0.0.255这一整个段的IP，禁止他们访问,其中10.0.0.0/24表示为从10.0.0.0这个IP开始,24代表子网掩码为255.255.255.0,共包含256个地址    

firewall-cmd --permanent --remove-rich-rule =“xxxx”  解除限制  

firewall-cmd --permanent --remove-port=3306/tcp  删除原有的3306端口访问规则   

firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address=" 192.168.1.100" port protocol="tcp" port="3306" accept"  添加规则



| cenos7 防火墙                       |                       |
| ----------------------------------- | --------------------- |
| systemctl stop firewalld.service    | #停止firewall         |
| systemctl disable firewalld.service | #禁止firewall开机启动 |
| firewall-cmd --state                | 查看防火墙状态        |



### Ubuntu 防火墙

Ubuntu 默认使用的是 `ufw` （Uncomplicated Firewall）作为防火墙

在 Ubuntu 中，`ufw` 防火墙规则保存在 `/etc/ufw` 目录下。该目录包含以下文件和目录：

- `/etc/ufw/ufw.conf` - `ufw` 的全局配置文件，包括默认行为和全局选项。
- `/etc/ufw/applications.d/` - 包含为特定应用程序定义防火墙规则的文件的目录。
- `/etc/ufw/before.rules` - 在 `ufw` 应用规则之前应用的规则。
- `/etc/ufw/after.rules` - 在 `ufw` 应用规则之后应用的规则。
- `/etc/ufw/before6.rules` - 在 `ufw` 应用 IPv6 规则之前应用的规则。
- `/etc/ufw/after6.rules` - 在 `ufw` 应用 IPv6 规则之后应用的规则。

如果您需要编辑 `ufw` 防火墙规则，建议备份这些文件，然后使用文本编辑器进行编辑。编辑后，您可以使用 `sudo ufw reload` 命令重新加载 `ufw` 防火墙规则

| ubuntu  防火墙                  |                                                              |
| ------------------------------- | ------------------------------------------------------------ |
| sudo ufw allow <port>/tcp       | 添加或修改防火墙规则, 其中 `<port>` 是您要开放的端口号，例如 `80` 或 `22`。此命令将允许从外部网络访问您的计算机上的指定端口。 |
| sudo ufw enable                 | 启用防火墙                                                   |
| sudo ufw disable                | 禁用防火墙                                                   |
| sudo ufw deny <port>/<protocol> | 禁止流量通过某个端口                                         |
| sudo ufw status                 | 防火墙状态                                                   |
|                                 |                                                              |
|                                 |                                                              |
|                                 |                                                              |
|                                 |                                                              |



# 8. ubuntu mysql

```
sudo apt update
```

 

自动安装mysql ubuntu20 默认安装mysql8

```
sudo apt install mysql-server  
```



一旦安装完成，MySQL 服务将会自动启动。想要验证 MySQL 服务器正在运行，输入:

```text
sudo systemctl status mysql
```



以 root 用户身份登录 MySQL服务器，输入:

```
sudo mysql
```



```
sudo service mysql status # 查看服务状态 

sudo service mysql start # 启动服务 

sudo service mysql stop # 停止服务 

sudo service mysql restart # 重启服务
```



查看密码

```
sudo cat /etc/mysql/debian.cnf
```






# 9. centos 与 Ubuntu





| 操作内容                   | Centos 6/7                                                   | Debian/Ubuntu                                                |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.软件包后缀               | *.rpm                                                        | *.deb                                                        |
| 2.软件源配置文件           | /etc/yum.conf                                                | /etc/apt/sources.list                                        |
| 3.更新软件包列表           | yum makecache fast                                           | apt-get update                                               |
| 4.从软件仓库安装软件       | yum install package                                          | apt-get install package                                      |
| 5.安装一个已下载的软件包   | yum install pkg.rpm rpm -i pkg.rpm                           | dpkg -i pkg.deb dpkg --install pkg.deb                       |
| 6.删除软件包               | rpm -e package yum remove package                            | apt-get remove package apt-get purge package                 |
| 7.获取某软件包的信息**     | yum search package                                           | apt-cache search package                                     |
| 8.获显示所有已经安装软件   | yum list installed rpm -qa                                   | dpkg -l dpkg --list                                          |
| 9.获取已经安装软件包的信息 | rpm -qi package                                              | dpkg --status packages                                       |
| 10.网卡配置文件            | /etc/sysconfig/network-scripts/ifcfg-eth0                    | /etc/network/interfaces                                      |
| 11.selinux                 | /etc/selinux/config                                          | 没有 selinux                                                 |
| 12.SSH                     | 默认允许 root 登陆                                           | 默认不允许 root 登陆                                         |
| 13.创建用户                | 默认创建用户家目录 默认 shell 解释器为 bash 免交互创建密码--stdin | 默认不创建用户家目录 默认 shell 解释器为 sh 免交互创建密码 chpasswd |
| 14.防火墙规则              | 默认规则                                                     | 默认没有任何规则                                             |
| 15.权限                    | root 或普通用户                                              | 默认普通用户权限                                             |



## 常用的apt-get命令参数



| apt-cache search package            | 搜索包                                 |
| ----------------------------------- | -------------------------------------- |
| apt-cache show package              | 获取包的相关信息，如说明、大小、版本等 |
| apt-cache depends package           | 了解使用依赖                           |
| apt-cache rdepends package          | 查看该包被哪些包依赖                   |
| apt-get install package             | 安装包                                 |
| apt-get install package --reinstall | 重新安装包                             |
| apt-get -f install                  | 修复安装"-f = --fix-missing"           |
| apt-get remove package              | 删除包                                 |
| apt-get remove package --purge      | 删除包，包括删除配置文件等             |
| apt-get update                      | 更新源                                 |
| apt-get upgrade                     | 更新已安装的包                         |
| apt-get dist-upgrade                | 升级系统                               |
| apt-get dselect-upgrade             | 使用 dselect 升级                      |
| apt-get build-dep package           | 安装相关的编译环境                     |
| apt-get source package              | 下载该包的源代码                       |
| apt-get clean && apt-get autoclean  | 清理无用的包                           |
| apt-get check                       | 检查是否有损坏的依赖                   |


# 10. 创建文件 文件夹

1. 如果要创建一个空文件，可以使用touch命令。如**"touch zuoyo"**
2. 如果vi 后面接的文件名不存在，会自动进入vi界面。意为创建一个文件





# 11. ubuntu redis



| command                      | description |      |
| ---------------------------- | ----------- | ---- |
| service redis-server start   | 启动redis   |      |
| service redis-server stop    | 关闭redis   |      |
| service redis-server restart | 重启redis   |      |
| service redis-server status  | 查看状态    |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |
|                              |             |      |



# 12. /bin/bash

   ![](H:\linux-study\img\20170404132212257.png)

 

>  第一行的内容指定了shell脚本解释器的路径，而且这个指定路径只能放在文件的第一行。第一行写错或者不写时，系统会有一个默认的解释器进行解释。





# 13. 文件命令

## 1. command

| command                                 | description                                    | example                                      |
| --------------------------------------- | ---------------------------------------------- | -------------------------------------------- |
| touch 新文件                            | 新建文件                                       |                                              |
| find (/查找范围) -name 文件名[文件夹名] | 查找文件                                       | find home -name nginx<br>find / -name nginx; |
| rm -rf \<文件 目录>                     | 强力删除, 不要求确认                           |                                              |
| rmdir 文件夹名                          | 删除文件夹                                     |                                              |
| rm 文件名                               | 删除文件                                       |                                              |
| rm -r 文件夹名                          | 递归删除文件夹及下面的所有文件和文件夹         |                                              |
| mv 原文件名 修改后的文件名              | 修改文件名                                     |                                              |
| unzip zip文件名                         | 解压zip文件                                    |                                              |
| unzip -d 指定目录名 要解压的文件        | -d 后接目录： 指定文件解压缩后所要存储的目录； | unzip  -d  /home/wg  test.jar                |
| tar -zxvf gz文件名                      | 解压gz文件                                     |                                              |
| tar                                     | -C 表示 换个文件夹                             | tar -zxvf typora.gz -C /home/wg/typora       |
| echo  >  文件名                         | 清除文件内容                                   | echo  >  文件名                              |
| sudo chmod -R 777 文件夹                | 给文件夹下所有文件 赋权限                      |                                              |
| shopt -s extglob                        | 开启 删除 除了 -s 开启 -u关闭                  |                                              |
| rm -f !(a)                              | 先执行上面的命令删除除了 a 之外的所有文件      |                                              |
| cp   -r  /home/wg/nacos   /usr/nacos    | 复制文件夹 -r 表示 递归复制                    |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |
|                                         |                                                |                                              |



## 2. tail

`tail` 命令通常用于查看文件的末尾内容，以下是 `tail` 命令的一些常见用法及参数解释：

1. 查看文件末尾内容

```
tail filename
```

该命令会在终端输出文件末尾的最后 10 行内容（默认值）。

1. 实时浏览文件变化

```
tail -f filename
```

该命令会打开文件，并持续输出新添加到文件末尾的内容。适用于需要实时监控日志等情景。

1. 显示指定数量的行数

```
tail -n [number] filename
```

该命令会显示指定数量 [number] 的行数（例如 -n 20 则显示文件末尾的最后 20 行内容）。

1. 从文件头开始显示内容

```
tail -r filename
```

该命令会从文件头开始显示内容，而不是文件尾。一般会和 `-n` 参数一起使用，如 `tail -n 20 -r filename`。

1. 组合使用多个参数

```
tail -fn [number] filename
```

该命令组合了 `-f` 和 `-n` 参数，在实时浏览文件变化的同时，也限制了回显的最大行数。

除了上述参数外，`tail` 还有很多其他用法，可通过 `man tail` 命令查看完整帮助文档



## 3. grep

`grep` 是一种文本搜索工具，用于在文件中查找指定字符串或正则表达式，并将匹配行输出到终端或保存在文件中。它的名称来自于 "global regular expression print" 的缩写。通常用法是结合管道符使用其他命令，如 `ls | grep "txt"` 匹配以 "txt" 结尾的文件并输出结果列表。



## 4. qa

1. 文件夹上带个箭头是啥意思?


   在Ubuntu中，当文件夹上有一个箭头，通常表示该文件夹是一个符号链接（symbolic link）或者软链接（soft link）。符号链接是一种特殊类型的文件，它包含指向另一个文件或文件夹的路径。当您点击这个带箭头的文件夹时，实际上会打开链接所指向的目标文件夹。

   符号链接提供了一种在文件系统中创建指向其他文件或目录的快捷方式的方式。它们允许您创建一个指向另一个位置的链接，使得您可以方便地访问其他位置的文件或文件夹，而无需在不同位置复制文件。

   当您在Ubuntu中创建一个符号链接时，文件夹图标上就会显示一个箭头，以区分它们与普通文件夹的不同。这样您可以快速辨认出它是一个链接，而不是一个实际的文件夹。

   请注意，符号链接可以是相对路径或绝对路径。相对路径是相对于当前位置的路径，而绝对路径是从根目录开始的完整路径。这取决于您创建符号链接时使用的路径。

2. 那这个带箭头的文件里面的内容 占用空间吗?

   在Ubuntu中，带箭头的文件夹是一个符号链接或软链接，它只是指向另一个位置的路径，并不包含实际的文件或文件夹内容。因此，它本身并不占用空间。

   当您打开带箭头的文件夹并访问链接所指向的目标位置时，您会看到目标位置中的文件和文件夹内容，并且它们会占用磁盘空间。实际的文件或文件夹内容位于目标位置，而不是带箭头的文件夹本身。

   因此，带箭头的文件夹只是一个指向其他位置的路径引用，不会占用额外的空间。它只是提供了一个方便的方式来访问其他位置的文件或文件夹。

3. 

# 14. 网络命令

  

| command        |                                                   |      |
| -------------- | ------------------------------------------------- | ---- |
| netstat        | 查端口号                                          |      |
| netstat -tunlp | 用于显示tcp udp的端口和进程情况, 详见下方命令解释 |      |
|                |                                                   |      |



# 15. 系统命令

  ## 1. command



| command                                                      |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| lsb_release -a                                               | 查看ubuntu版本                                               |                                                              |
| dpkg                                                         | Debian Packager ”的简写, 为 “Debian” 专门开发的套件管理系统，方便软件的安装、更新及移除, 所有源自“Debian”的“Linux ”发行版都使用 “dpkg”，例如 “Ubuntu”、“Knoppix ”等。 |                                                              |
| apt                                                          | Advanced Package Tool, 命令并不直接操作 deb 安装包文件，而是从 /etc/apt/sources.list 配置文件中定义的软件镜像源里下载软件包并安装，使用时也只需指定软件的名称（或者也可以附加上版本号）。**因此，dpkg 主要是用来安装已经下载到本地的 deb 软件包，或者对已经安装好的软件进行管理。而 apt-get 可以直接从远程的软件仓库里下载安装软件** |                                                              |
| systemd-analyze blame                                        | 查看开机启动项                                               |                                                              |
| systemd is-enabled redis.service                             | 查看 redis 是否开机启动                                      |                                                              |
| pwd                                                          | 查看当前位置                                                 |                                                              |
| tail -f 文件名                                               | 查看文件详情                                                 | tail -f nohup.out                                            |
| ps -ef\|grep 进程名                                          | 查看进程                                                     | ps -ef\|grep java                                            |
| pstree                                                       | 树状显示进程                                                 |                                                              |
| ps  aux                                                      | 显示进程                                                     |                                                              |
| cat /proc/meminfo                                            | 查看内存信息命令                                             |                                                              |
| fdisk -l                                                     | 查看硬盘信息命令                                             |                                                              |
| sudo cat /etc/mysql/debian.cnf                               | 查看 自动安装的 mysql 密码                                   |                                                              |
| cat /etc/passwd                                              | 查看用户信息                                                 | 用户名：密码占位符（x 表示用户需要密码登录）：用户标识号（`UID`）：<br/>组标识号（`GID`）：注释性描述：主目录：登录的 `shell` |
| cat /etc/shadow                                              | 查看用户密码                                                 |                                                              |
| cat /etc/group                                               | 查看用户组                                                   | 组名 : 口令 : 组标识号（`GID`）：组内用户列表（多用户可用逗号分隔开） |
| cat  /proc/cpuinfo                                           | 查看cpu 信息                                                 |                                                              |
| echo                                                         | 显示文字                                                     | echo $PATH    // 显示 path                                   |
| update-alternatives --config java                            | 切换Java版本, 能看到java 的安装位置                          |                                                              |
| source /etc/profile                                          | 让配置生效                                                   |                                                              |
| shopt -s extgolb                                             | 开启 特定文件的删除或 除了 某些文件 删除其他的文件; 打开扩展的模式匹配特性(正常的表达式元字符来自Korn shell的文件名扩展) |                                                              |
| firewall-cmd --zone=public  --list-ports                     | 查看已经对外开放的端口                                       |                                                              |
| firewall-cmd --zone=public --add-port=8080/tcp --permanent   | 添加开放对外的端口(8080)                                     |                                                              |
| firewall-cmd --reload                                        | 重新载入一下防火墙设置，使设置生效                           |                                                              |
| firewall-cmd --zone=public --query-port=2228/tcp             | 通过命令查看是否生效                                         |                                                              |
| firewall-cmd --zone=public --remove-port=80/tcp --permanent  | 关闭80/tcp端口                                               |                                                              |
| firewall-cmd --zone=public --add-port=40000-45000/tcp --permanent | 批量开放端口，打开从40000到45000之间的所有端口               |                                                              |
| firewall-cmd --zone=public --remove-port=40000-45000/tcp --permanent | 批量关闭端口，关闭从40000到45000之间的所有端口               |                                                              |
| apt-get --purge remove 程序名                                | 删除某程序                                                   |                                                              |
| hostname   -I                                                | 大写的i , 查本机ip                                           |                                                              |
| id  -g  <username>                                           | 查询用户的组id                                               |                                                              |
| id -G <username>                                             | 查询该用户属于哪些其他组                                     |                                                              |
| uname  -a                                                    | 查询系统内核版本和主机名等信息                               |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |



## 2. 详细说明

### 1. shopt

 shopt = shell options

shopt 命令用于显示和设置shell中的行为选项，通过这些选项以增强shell易用性。

简介

shopt [-psu] [optname …]

-s 开启某个选项.

-u 关闭某个选项.

-p 列出所有可设置的选项.



```shell
[root@master four]# shopt
autocd         	off
cdable_vars    	off
cdspell        	off
checkhash      	off
checkjobs      	off
checkwinsize   	on
cmdhist        	on
compat31       	off
compat32       	off
compat40       	off
dirspell       	off
dotglob        	off
execfail       	off
expand_aliases 	on
extdebug       	off
extglob        	on
extquote       	on
failglob       	off
force_fignore  	on
globstar       	off
gnu_errfmt     	off
histappend     	off
histreedit     	off
histverify     	off
hostcomplete   	on
huponexit      	off
interactive_comments	on
lithist        	off
login_shell    	on
mailwarn       	off
no_empty_cmd_completion	off
nocaseglob     	off
nocasematch    	off
nullglob       	off
progcomp       	on
promptvars     	on
restricted_shell	off
shift_verbose  	off
sourcepath     	on
xpg_echo       	off
[root@master four]# shopt
autocd         	off
cdable_vars    	off
cdspell        	off
checkhash      	off
checkjobs      	off
checkwinsize   	on
cmdhist        	on
compat31       	off
compat32       	off
compat40       	off
dirspell       	off
dotglob        	off
execfail       	off
expand_aliases 	on
extdebug       	off
extglob        	on
extquote       	on
failglob       	off
force_fignore  	on
globstar       	off
gnu_errfmt     	off
histappend     	off
histreedit     	off
histverify     	off
hostcomplete   	on
huponexit      	off
interactive_comments	on
lithist        	off
login_shell    	on
mailwarn       	off
no_empty_cmd_completion	off
nocaseglob     	off
nocasematch    	off
nullglob       	off
progcomp       	on
promptvars     	on
restricted_shell	off
shift_verbose  	off
sourcepath     	on
xpg_echo       	off
```

### 2. dpkg

dpkg = Debian Packager

dpkg --list: 

```shell

期望状态=未知(u)/安装(i)/删除(r)/清除(p)/保持(h)
| 状态=未安装(n)/已安装(i)/仅存配置(c)/仅解压缩(U)/配置失败(F)/不完全安装(H)/触发器等待(W)/触发器未决(T)
|/ 错误?=(无)/须重装(R) (状态，错误：大写=故障)
||/ 名称                                       版本                                  体系结构     描述
+++-==========================================-=====================================-============-======================================================================================================
ii  accountsservice                            0.6.55-0ubuntu12~20.04.5              amd64        query and manipulate user account information
ii  acl                                        2.2.53-6                              amd64        access control list - utilities
ii  acpi-support                               0.143                                 amd64        scripts for handling many ACPI events
ii  acpid                                      1:2.0.32-1ubuntu1                     amd64        Advanced Configuration and Power Interface event daemon
ii  adduser                                    3.118ubuntu2                          all          add and remove users and groups

```



dpkg --help: 

```shell

命令：
  -i|--install       <.deb 文件名> ... | -R|--recursive <目录> ...
  --unpack           <.deb 文件名> ... | -R|--recursive <目录> ...
  -A|--record-avail  <.deb 文件名> ... | -R|--recursive <目录> ...
  --configure        <软件包名>    ... | -a|--pending
  --triggers-only    <软件包名>    ... | -a|--pending
  -r|--remove        <软件包名>    ... | -a|--pending
  -P|--purge         <软件包名>    ... | -a|--pending
  -V|--verify <软件包名> ...       检查包的完整性。
  --get-selections [<表达式> ...]  把已选中的软件包列表打印到标准输出。
  --set-selections                 从标准输入里读出要选择的软件。
  --clear-selections               取消选中所有不必要的软件包。
  --update-avail <软件包文件>      替换现有可安装的软件包信息。
  --merge-avail  <软件包文件>      把文件中的信息合并到系统中。
  --clear-avail                    清除现有的软件包信息。
  --forget-old-unavail             忘却已被卸载的不可安装的软件包。
  -s|--status      <软件包名> ...  显示指定软件包的详细状态。
  -p|--print-avail <软件包名> ...  显示可供安装的软件版本。
  -L|--listfiles   <软件包名> ...  列出属于指定软件包的文件。
  -l|--list  [<表达式> ...]        简明地列出软件包的状态。
  -S|--search <表达式> ...         搜索含有指定文件的软件包。
  -C|--audit [<表达式> ...]        检查是否有软件包残损。
  --yet-to-unpack                  列出标记为待解压的软件包。
  --predep-package                 列出待解压的预依赖。
  --add-architecture    <体系结构> 添加 <体系结构> 到体系结构列表。
  --remove-architecture <体系结构> 从架构列表中移除 <体系结构>。
  --print-architecture             显示 dpkg 体系结构。
  --print-foreign-architectures    显示已启用的异质体系结构。
  --assert-<特性>                  对指定特性启用断言支持。
  --validate-<属性> <字符串>       验证一个 <属性>的 <字符串>。
  --compare-vesions <a> <关系> <b> 比较版本号 - 见下。
  --force-help                     显示本强制选项的帮助信息。
  -Dh|--debug=help                 显示有关出错调试的帮助信息。

  -?, --help                       显示本帮助信息。
      --version                    显示版本信息。

Assert 特性： support-predepends, working-epoch, long-filenames,
  multi-conrep, multi-arch, versioned-provides.

可验证的属性：pkgname, archname, trigname, version.

调用 dpkg 并带参数 -b, --build, -c, --contents, -e, --control, -I, --info,
  -f, --field, -x, --extract, -X, --vextract, --ctrl-tarfile, --fsys-tarfile
是针对归档文件的。 (输入 dpkg-deb --help 获取帮助)

选项：
  --admindir=<目录>          使用 <目录> 而非 /var/lib/dpkg。
  --root=<目录>              安装到另一个根目录下。
  --instdir=<目录>           改变安装目录的同时保持管理目录不变。
  --path-exclude=<表达式>    不要安装符合Shell表达式的路径。
  --path-include=<表达式>    在排除模式后再包含一个模式。
  -O|--selected-only         忽略没有被选中安装或升级的软件包。
  -E|--skip-same-version     忽略版本与已安装软件版本相同的软件包。
  -G|--refuse-downgrade      忽略版本早于已安装软件版本的的软件包。
  -B|--auto-deconfigure      就算会影响其他软件包，也要安装。
  --[no-]triggers            跳过或强制随之发生的触发器处理。
  --verify-format=<格式>     检查输出格式('rpm'被支持)。
  --no-debsig                不去尝试验证软件包的签名。
  --no-act|--dry-run|--simulate
                             仅报告要执行的操作 - 但是不执行。
  -D|--debug=<八进制数>      开启调试(参见 -Dhelp 或者 --debug=help)。
  --status-fd <n>            发送状态更新到文件描述符<n>。
  --status-logger=<命令>     发送状态更新到 <命令> 的标准输入。
  --log=<文件名>             将状态更新和操作信息到 <文件名>。
  --ignore-depends=<软件包>,...
                             忽略关于 <软件包> 的所有依赖关系。
  --force-...                忽视遇到的问题(参见 --force-help)。
  --no-force-...|--refuse-...
                             当遇到问题时中止运行。
  --abort-after <n>          累计遇到 <n> 个错误后中止。

可供--compare-version 使用的比较运算符有：
 lt le eq ne ge gt        (如果版本号为空，那么就认为它先于任意版本号)；
 lt-nl le-nl ge-nl gt-nl  (如果版本号为空，那么就认为它后于任意版本号)；
 < << <= = >= >> >        (仅仅是为了与主控文件的语法兼容)。

'apt' 和 'aptitude' 提供了更为便利的软件包管理。
```



|                                                 |                                |      |
| ----------------------------------------------- | ------------------------------ | ---- |
| dpkg --list \| grep ^rc                         | 查看处于 `rc` 状态的软件包：   |      |
| dpkg --purge 程序名                             | 删除程序, 并删除其配置文件     |      |
| dpkg -s <package> 或 dpkg --status <package>    | 查看软件包（已安装）的详细信息 |      |
| dpkg -L <package> 或 dpkg --listfiles <package> | 查看软件包的安装位置           |      |
|                                                 |                                |      |
|                                                 |                                |      |
|                                                 |                                |      |
|                                                 |                                |      |
|                                                 |                                |      |



### 3. grep

grep =  Global Regular Expression Print

命令用于查找文件里符合条件的字符串。grep 指令用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的范本样式，预设 grep 指令会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为 **-**，则 grep 指令会从标准输入设备读取数据。



在当前目录中，查找后缀有 file 字样的文件中包含 test 字符串的文件，并打印出该字符串的行。此时，可以使用如下命令

```shell
grep "test" *file
```



|                             |                                                              |      |
| --------------------------- | ------------------------------------------------------------ | ---- |
| grep "mysql" /etc/passwd    | 查找 mysql 字符串 在 /etc/passwd 文件里                      |      |
| grep -v "mysql" /etc/passwd | 查询 没有 mysql 的行 , 我们使用`-v`选项实现了反查效果，可以看到，含有 mysql 的行都没有展示出来。 |      |
|                             |                                                              |      |



```shell
wg@wg-Aspire-A315-55G:~$ grep --help
用法: grep [选项]... 模式 [文件]...
在每个<文件>中查找给定<模式>。
例如：grep -i 'hello world' menu.h main.c
<模式>可以包括多个模式字符串，使用换行符进行分隔。

模式选择与解释：
  -E, --extended-regexp     <模式> 是扩展正则表达式
  -F, --fixed-strings       <模式> 是字符串
  -G, --basic-regexp        <模式> 是基本正则表达式
  -P, --perl-regexp         <模式> 是 Perl 正则表达式
  -e, --regexp=<模式>       用指定的<模式>字符串来进行匹配操作
  -f, --file=<文件>         从给定<文件>中取得<模式>
  -i, --ignore-case         在模式和数据中忽略大小写
      --no-ignore-case      不要忽略大小写（默认）
  -w, --word-regexp         强制<模式>仅完全匹配字词
  -x, --line-regexp         强制<模式>仅完全匹配整行
  -z, --null-data           数据行以一个 0 字节结束，而非换行符

杂项:
  -s, --no-messages         不显示错误信息
  -v, --invert-match        选中不匹配的行
  -V, --version             显示版本信息并退出
      --help                显示此帮助并退出

输出控制：
  -m, --max-count=<次数>    得到给定<次数>次匹配后停止
  -b, --byte-offset         输出的同时打印字节偏移
  -n, --line-number         输出的同时打印行号
      --line-buffered       每行输出后刷新输出缓冲区
  -H, --with-filename       为输出行打印文件名
  -h, --no-filename         输出时不显示文件名前缀
      --label=<标签>        将给定<标签>作为标准输入文件名前缀
  -o, --only-matching       只显示行中非空匹配部分
  -q, --quiet, --silent     不显示所有常规输出
      --binary-files=TYPE   设定二进制文件的 TYPE（类型）；
                            TYPE 可以是 'binary'、'text' 或 'without-match'
  -a, --text                等同于 --binary-files=text
  -I                        等同于 --binary-files=without-match
  -d, --directories=ACTION  读取目录的方式；
                            ACTION 可以是`read', `recurse',或`skip'
  -D, --devices=ACTION      读取设备、先入先出队列、套接字的方式；
                            ACTION 可以是`read'或`skip'
  -r, --recursive           等同于--directories=recurse
  -R, --dereference-recursive       同上，但遍历所有符号链接
      --include=GLOB        只查找匹配 GLOB（文件模式）的文件
      --exclude=GLOB        跳过匹配 GLOB 的文件
      --exclude-from=FILE   跳过所有匹配给定文件内容中任意模式的文件
      --exclude-dir=GLOB    跳过所有匹配 GLOB 的目录
  -L, --files-without-match  只打印没有匹配上的<文件>的名称
  -l, --files-with-matches  只打印有匹配的<文件>的名称
  -c, --count               只打印每个<文件>中的匹配行数目
  -T, --initial-tab         行首制表符对齐（如有必要）
  -Z, --null                在<文件>名最后打印空字符

文件控制:
  -B, --before-context=NUM  打印文本及其前面NUM 行
  -A, --after-context=NUM   打印文本及其后面NUM 行
  -C, --context=NUM         打印NUM 行输出文本
  -NUM                      等同于 --context=NUM
      --color[=WHEN],
      --colour[=WHEN]       使用标记高亮匹配字串；
                            WHEN 可以是“always”、“never”或“auto”
  -U, --binary              不要清除行尾的 CR 字符（MSDOS/Windows）

若给定<文件>为“-”，则从读取标准输入。  若无<文件>参数，则除非处于
递归工作模式视为从“.”读取之外，一律视为从“-”读取。如果提供了少于
两个<文件>参数，则默认启用 -h 选项。如果有任意行（或者指定了 -L 选项
并有任意文件）被匹配，则退出状态为 0，否则为 1；如果有错误产生，且未指
定 -q 参数，则退出状态为 2。

请将错误报告给：bug-grep@gnu.org。翻译问题请报告至 <i18n-zh@googlegroups.com>。
GNU grep 主页: <http://www.gnu.org/software/grep/>
GNU 软件的通用帮助: <https://www.gnu.org/gethelp/>

```



### 4. ps

ps = process status 

用于显示当前进程的状态，类似于 windows 的任务管理器。



ps -ef | grep redis

```tex
参数 -e  显示运行在系统上的所有进程

参数 -f  扩展显示输出

中间的|是管道命令 是指ps命令与grep同时执行
```



# 16. 权限

 例: 

```shell
drwxr-xr-x   2 root root  4096 2009-01-14 17:34 bin 
```

其中 drwxr-xr-x 共 10位, 以0-9为序号

其中 0位 : [ d ]–目录、[ - ]–文件、[ l ]–链接、[ b ]–可储存周边设备、[ c ]–序列设备

123位: 表示拥有人的权限

456位: 表示同组群使用者权限

789位: 表示其他使用者权限

---

r、w、x也有对应的数字：
r—4
w—2
x—1

5=4 + 1,表示拥有可读,可执行权限，但是没有写权限

7=4+2+1, 表示可读,可写,可执行权限

```shell
# 可看权限
ls -l [文件名]
```



|      |                                              |      |
| ---- | -------------------------------------------- | ---- |
| 600  | 只有所有者有读和写的权限                     |      |
| 644  | 只有所有者有读和写的权限，组用户只有读的权限 |      |
| 700  | 只有所有者有读和写以及执行的权限             |      |
| 666  | 每个人都有读和写的权限                       |      |
| 777  | 每个人都有读和写以及执行的权限               |      |
| 774  | 其他人只能读                                 |      |
| 664  | 其他人只能读                                 |      |



# 17. 语法

命令格式中常用的几个符号含义如下：

尖括号< >：必选参数，实际使用时应将其替换为所需要的参数

大括号{ }：必选参数，内部使用，包含此处允许使用的参数

方括号[ ]：可选参数，在命令中根据需要加以取舍

小括号( )：指明参数的默认值，只用于{ }中

竖线|：用于分隔多个互斥参数，含义为“或”，使用时只能选择一个。

省略号…：任意多个参数。



# 18. 符号

## 1. ">>"

这个符号

`>>` 是 Shell 中的追加输出符号，与 `>` 的作用不同，`>` 会将原来的文件内容清空并重新写入新的内容。

```
echo "sdfsd" >> wg.txt
```

这条命令的作用是将字符串 "sdfsd" 追加到文件 wg.txt 的末尾，而不会覆盖已有的内容。`>>` 是 Shell 中的追加输出符号，与 `>` 的作用不同，`>` 会将原来的文件内容清空并重新写入新的内容。

如果 wg.txt 文件不存在，则该命令将自动创建一个新文件，并在其中添加字符串 "sdfsd"。如果 wg.txt 已经存在，则会将字符串追加到文件末尾，而不影响原有的内容。

需要注意的是，如果文件已经被其他进程打开，在进行追加操作时可能会出现并发访问问题。为了避免这种情况，可以使用文件锁或其他同步机制来保证安全性



# 19. gitlab-runner 安装

```
# Linux x86-64
sudo curl -L --output /usr/local/bin/gitlab-runner "https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64"

sudo chmod +x /usr/local/bin/gitlab-runner

sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

sudo gitlab-runner install --working-directory=/home/gitlab-runner
sudo gitlab-runner start

gitlab-runner register --url http://gitlab.sevenme.com/ --registration-token GR1348941zeUGWbz5-uUQZmdnVYYt
```



# 20. k8s安装

安装 kubectl

```shell
curl -LO https://dl.k8s.io/release/v1.27.1/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl completion bash
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
sudo chmod a+r /etc/bash_completion.d/kubectl
```



安装 kubectl-convert 插件

```
# 安装文件
curl -LO "https://dl.k8s.io/release/v1.27.1/bin/linux/amd64/kubectl-convert"

# 验证文件
curl -LO "https://dl.k8s.io/v1.27.1/bin/linux/amd64/kubectl-convert.sha256"

# 验证命令
echo "$(cat kubectl-convert.sha256) kubectl-convert" | sha256sum --check

# 安装
sudo install -o root -g root -m 0755 kubectl-convert /usr/local/bin/kubectl-convert

# 验证是否成功
kubectl convert --help

# 完成后, 删除安装文件
rm kubectl-convert kubectl-convert.sha256
```



# 21. java 切换版本

1. 查询

   ```
   sudo update-alternatives --display java
   ```

2. 切换

   ```
   sudo update-alternatives --config java
   ```

3. edit /etc/profile

4. 如果找不到 

   ```
   which java
   /usr/bin/java
   ls -lrt /usr/bin/java
   /usr/bin/java -> /etc/alternatives/java
   ls -lrt /etc/alternatives/java
   /etc/alternatives/java -> /usr/lib/jvm/java-11-openjdk-amd64/bin/java
   ```

   