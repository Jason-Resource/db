# 先安装依赖
yum -y install libevent libevent-deve

# 安装memcached
yum -y install memcached

# 查看安装在哪里（一般安装在/usr/bin目录下）
whereis memcached

# 启动
/usr/bin/memcached -uroot -d

# 查看启动端口
netstat -an | grep 11211

# 查看启动PID
ps -ef | grep memcached

# 查看启动进程树
pstree -p | grep memcached

# 安装telnet
yum -y install telnet

# telnet连接
telnet localhost 11211

# 存数据
set name 0 900 5
jason

# 取数据
get name

# 退出telnet
quit
