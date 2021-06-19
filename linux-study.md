# 1. 一些命令



| <span style="white-space: nowrap">命令 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;&emsp;&emsp;&emsp;</span> | <span style="white-space: nowrap">说明 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;</span> | <span style="white-space: nowrap">例子 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;</span> |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ps -ef\|grep 进程名                                          | 查看进程                                                     | ps -ef\|grep java                                            |
| tail -f 文件名                                               | 查看文件详情                                                 | tail -f nohup.out                                            |
| nohup java -jar jar包 > nohup.out 2>&1 &                     | jar包 部署命令 , jar包> 后面 有空格, 详见下方命令解释        | nohup java -jar mahua.jar   > nohup.out 2>&1 &               |
| kill -9 进程号                                               | 杀 进程, 不给反应时间的杀                                    |                                                              |
| find (/查找范围) -name 文件名/文件夹名                       | 查找文件                                                     | find home -name nginx<br>find / -name nginx;                 |
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
| unzip zip文件名                                              | 解压zip文件                                                  |                                                              |
| tar -zxvf gz文件名                                           | 解压gz文件                                                   |                                                              |
| unzip 壓縮包名                                               | 解壓zip文件                                                  |                                                              |
| unzip -d 指定目录名 要解压的文件                             | -d 后接目录： 指定文件解压缩后所要存储的目录；               |                                                              |
| ln -s  源文件 目标文件                                       | 为某一个文件在另外一个位置建立一个同不的链接，这个命令最常用的参数是-s |                                                              |
| sudo apt autoremove                                          | 清理系统                                                     |                                                              |
| find . -type d -empty -delete                                | 删除所有空目录                                               |                                                              |
| sudo apt-get -f install                                      | 修复依赖包                                                   |                                                              |
| systemctl disable 服务名                                     | 禁止开机启动服务                                             |                                                              |
| systemctl enable 服务名                                      | 开启开机启动服务                                             |                                                              |
| shutdown -r now                                              | 立即重启                                                     |                                                              |
| shutdown -h now                                              | 关机                                                         |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |
|                                                              |                                                              |                                                              |



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
| usr                     | 要用到的应用程序和文件几乎都在这个目录                       |
| /usr/share/applications | 桌面图标的位置                                               |
| /lib                    | apt 安装的程序 如 jvm mysql  都在这个文件夹下                |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |



# 3. 缩写

| 简写  | 全称                 | 解释                                                       |
| ----- | -------------------- | ---------------------------------------------------------- |
| su    | switch user          | 切换用户<br>使用su的缺点之一在于必须要先告知超级用户的密码 |
| sudo  | switch user do       | sudo使一般用户不需要知道超级用户的密码即可获得权限         |
| pwd   | print work direcory  | 打印工作目录, 显示当前位置                                 |
| ps    | process status       | 进程状态                                                   |
| rm    | remove               | 删除                                                       |
| rmdir | remove directory     | 删除目录                                                   |
| man   | manual               | 手册                                                       |
| ln -s | link -soft           | 创建快捷方式                                               |
| /usr  | unix shared resource | unix共享资源                                               |
| /proc | processes            | 进程                                                       |
| etc   |                      |                                                            |
| nohup | no hang up           | 不挂断                                                     |





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

1. nohup java -jar tientsineye.jar > tientsineye.out 2>&1 &

2. ```c
   nohup java -jar *.jar --spring.config.location=config/application.properties >*.log&
   ```

| command                                   | describle                                                    |
| ----------------------------------------- | ------------------------------------------------------------ |
| nohup                                     | 守护进程                                                     |
| java -Duser.timezone=GMT+8  -jar *.jar    | jar包启动, 使用 东八区区时, centos7 有这个问题, java 程序获取的时间 不对应 |
| --spring.config.location=配置文件(带路径) | 指定jar包读取的外部的配置文件                                |
| \>*.log                                   | 日志输出位置                                                 |
| 2>&1 &                                    | 2>&1是将标准错误（2）重定向到标准输出（&1），标准输出（&1）再被重定向输入到*.log文件中。 |
| &                                         | 守护进程(仅当前连接linux终端用户在线时，一旦该用户断开连接，项目将自动停止，因此需要使用nohup) |



2. netstat -tunlp

- -t (tcp) 仅显示tcp相关选项
- -u (udp)仅显示udp相关选项
- -n 拒绝显示别名，能显示数字的全部转化为数字
- -l 仅列出在Listen(监听)的服务状态
- -p 显示建立相关链接的程序名













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





# 9. 创建文件 文件夹

1. 如果要创建一个空文件，可以使用touch命令。如**"touch zuoyo"**
2. 如果vi 后面接的文件名不存在，会自动进入vi界面。意为创建一个文件





# 10 ubuntu redis



|                              |           |      |
| ---------------------------- | --------- | ---- |
| service redis-server start   | 启动redis |      |
| service redis-server stop    | 关闭redis |      |
| service redis-server restart | 重启redis |      |
| service redis-server status  | 查看状态  |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |
|                              |           |      |

