1）基础快捷键
ctrl + c 停止进程 
ctrl+l 清屏；彻底清屏是： reset 
ctrl + q 退出 
善于用 tab键补全 提示 (更重要的是可以防止敲错 ) 
上下键 查找执行过的命令
ctrl +alt
2）文件命令
#pwd 显示当前工作目录的绝对路径
#ls,ll,ll -a 
#cd 进入到某一个目录下
#mkdir 创建文件夹 
#rmdir 删除文件夹 
#touch 创建文件 
#cp 复制文件 /文件夹 
#cp -r 递归复制，多级目录
#mv 移动文件 夹/重命名
#rm 删除文件 
#rm -rf 强制删除文件不需要确认
#cat 查看文件
#more 查看文件
#less 查看文件
#echo 输出 #head 查看文件头部
#tail 查看文件末尾
#tail -f 实时查看文件末尾
#nl 文件带行号标准输出
# > 覆盖 
# >> 追加
#ln -s 目标目录 软链接地址 创建 软链接
rm -rf 软链接地址 删除软连接
ln -snf 新目标目录 软链接地址 修改软连接
# history 查看已经执行过历史命令
3）文本处理类命令
wc [option] [file]... 
    -l: 统计行数 
    -c: 统计字节数 
    -w；统计单词数

tr: 转换字符或删除字符 
    tr '集合 1' '集合 2' 
    tr -d '字符集合 '

cut:
    -d字符：指定分隔符   
    -f#: 指定要显示字段   
    单个数字：一个字段   
    逗号分隔的多个数字：指定多个离散字段   
    -：连续字段，如 3-5；
    例子：cut test.txt -f "1,3" -d " "------# 以空格分开每一行并输出第 1个和第 3个字段

sort [option] file... 
    -f: 忽略字符大小写；
    -n: 比较数值大小；
    -t: 指定分隔符 
    -k: 指定分隔后进行比较字段
    -u: 重复的行，只显示一次；
uniq:移除重复的行
    -c：显示每行重复的次数
    -d：仅显示重复过的行
    -u: 仅显示不曾重复的行


4）系统信息命令
#date 查看当前系统时间
#data -s 修改时间 
#w 显示登陆用户
#uname -a 查看系统内核
#cat /proc/cpuinfo 查看 cpu信息 
#cat /proc/meminfo 查
5）压缩/解压命令
#tar -xvf file.tar 解压 .tar结尾的 
#tar -zxvf file.tar.gz 解压 .tar.gz文件 
#tar -cf file.tar file 创建包含 files的文件 file.tar 
#gzip -d file.gz 将 file.gz解压缩为 file
6）网络命令
#ping host(主机名 ) 网络是否连通 
#telnet ip 端口  网络是否连通
#curl url 调用
#ifconfig 查看本机 ip等信息
#telnet ip 端口 查看端口是否占用
(没有这个命令执行 yum -y install telnet ) 
#wget file 下载文件 
#tcpdump tcp port 端口 抓包 tcp
#hostname  查看主机名
7）权限命令
1.文件权限命令：
#chmod 777 file 为所有用户添加读，写，执行权限
#chmod 755 file 为所有者添加 rwx权限，为组和其他用户添加
rx权限 
2.文件所属用户和用户组权限命令：
#chown hadoop:hadoop file 将 file的用户和用户组都改为 hadoop
8）用户管理命令
useradd 用户名 添加新用户 
useradd -g 组名 用户名 给某个组创建用户
passwd 用户名 设置用户密码 
cat /etc/passwd 查看创建了那些用户
Su 用户名 切换用户 
userdel 用户名 删除用户但保存用户主目录
userdel -r 用户名 用户和用户主目录，都删除
whoami 显示自身用户名称
who am i 显示登录用户的用户名
usermod -g 更改用户组 用户名


例子：
2．修改配置文件
[root@hadoop101 ~]#vi /etc/sudoers 修改 /etc/sudoers 文件，找到下面一行 (91行)，在 root下面添加一行，
如下所示：
## Allow root to run any commands anywhere 
root ALL=(ALL) ALL 
hadoopALL=(ALL) ALL 
或者配置成采用 sudo命令时，不需要输入密码
## Allow root to run any commands anywhere 
root ALL=(ALL) ALL 
hadoopALL=(ALL) NOPASSWD:ALL 
修改完毕，现在可以用 hadoop帐号登录，然后用命令 sudo ，即可 获得 root权限进行操作。
9）用户组管理命令
groupadd 组名 添加组
groupdel 组名 删除组
groupmod -n 新组名 老组名 指定工作组的新组名
cat /etc/group 查看创建了哪些组
10）搜索查找命令
1.find查找文件或者目录
    常用： find / -name file 查找 /目录下 file文件
2.grep 过滤查找及“ “|”管道符 （详细使用见下一章中的 grepgrep）
    1.管道符，“ ，“|”，表示将前一个命令的处理结果输出传递给后面的命令处理
    2.grep常常跟在 |的后面做过滤查找
    3.反转 grep -v 
    4.示例 
        #查找某文件在第几行 ls | grep -n test 
        #查找某进程 ps -ef | grep PID 
        #查看日志中含有 errer cat file |grep error
3.which 查找命令
    white 命令
11）磁盘分区挂载命令
df -h 查看磁盘使用 /剩余空间 
fdisk -l 磁盘分区
mount 挂载
umount 卸载
12）进程管理命令
UID 用户 ID 
PID 进程 ID 
ps aux | grep xxx 查看系统中所有进程
ps -ef | grep xxx 可以查看子父进程之间的关系
kill -9 PID 强制杀死进程
top 查看所有进程 /cpu/内存 /负载 
netstat -anp |grep 进程号 查看该进程网络信息
netstat -nlp | grep 端口号 查看网络端口号占用情况
13）crond系统定时任务
Crontab -e 编辑定时文件

参考文档：https://blog.csdn.net/qq_22172133/article/details/81263736

14）rpm包管理与yum管理
1.rpm相关命令：
rpm -qa|grep 包名 查找已经安装的 rpm某包 
rpm -ivh 包名 安装 rpm包 
rpm -e 包名 删除 rpm包 
rpm -e -- nodeps 软件包 删除 rpm包不检查依赖
2.yum源管理：详情见链接文档
https://blog.csdn.net/qingfenggege/article/details/80394564 
3.yum在线安装 lrzsz上传下载工具
yum -y install lrzsz

