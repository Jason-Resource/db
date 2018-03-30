/sbin/iptables -I INPUT -p tcp --dport 6379 -j ACCEPT
iptables -F


## 直接禁用防火墙
service iptables stop
