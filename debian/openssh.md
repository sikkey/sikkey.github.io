# 安装 openssh
```
sudo apt-get install openssh-server
```
部分系统没有安装client
```
sudo apt-get install openssh-client openssh-server
```

# 查看TCP端口22
```
# netstat -tulpn | grep :22
```

# 连接到Openssh服务器

```
$ ssh user@localhost
$ ssh user@sever-ip-here
```


# 在Debian Linux下启动/停止/重启OpenSSH服务器
```
# service ssh stop
# service ssh start
# service ssh restart
# service ssh status

# /etc/init.d/ssh stop
# /etc/init.d/ssh start
# /etc/init.d/ssh restart
# /etc/init.d/ssh status
```

# 防火墙级别打开端口22
编辑防火墙脚本并附加以下规则以限制对192.168.1.0/24的访问：
```
/sbin/iptables -A INPUT -s 192.168.1.0/24 -m state --state NEW -p tcp --dport 22 -j ACCEPT
```
保存并关闭文件。或者，您可以按如下方式键入命令并将其保存到防火墙配置文件中：
```
＃/sbin/iptables -A INPUT -s 192.168.1.0/24 -m state --state NEW -p tcp --dport 22 -j ACCEPT
＃iptables-save > /path/to/your.firewall.conf
```

# 在Debian配置和保护OpenSSH服务器
```
# vi /etc/ssh/sshd_config
```
