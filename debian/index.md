# Debian 操作汇总

[Complex Punk Blog](http://sikkey.github.io/)

# Debian 操作系统的下载与安装

[Debian 官方网站](https://www.debian.org/)

[Debian 10 安装手册](https://www.debian.org/releases/stable/arm64/install.pdf.zh-cn)

[Debian arm 移植](https://www.debian.org/ports/arm/)

[Debian live 映像](https://www.debian.org/CD/live/)   (:-P)类似WINDOWS PE

[Debian 10.4 AMD64 安装映像](http://http.us.debian.org/debian/dists/buster/main/installer-arm64/current/images/)

# Debian 切换为root用户
```
# su
```
输入命令后提示输入密码，输入密码切换为root用户

# Debian普通用户添加sudo权限

1、安装sudo
```
# apt-get install sudo
```
2、修改 /etc/sudoers 文件属性为可写
```
# chmod +w /etc/sudoers
```
3、编辑 /etc/sudoers ,添加如下行
```
# vim /etc/sudoers
root ALL=(ALL) ALL
user ALL=(ALL) ALL 用户user执行sudo时需要密码。
#user ALL=NOPASSWD:ALL 用户user执行sudo时不需要密码。
#user ALL=NOPASSWD:/etc/network/interfaces 用户user执行只有sudo执行/etc/network/interfaces的权限，执行时不需要密码。
```
4、修改/etc/sudoers 文件属性为只读
```
# chmod -w /etc/sudoers
```

# Debian 更新源
[apt-get 更新源](./apt.md)

# Debian 初始化安装

安装vim，unzip

```
sudo apt-get install vim unzip
```

安装 ssh
```
sudo apt install openssh-server
```

安装完成后SSH 服务默认开启
手动启动：
```
systemctl start ssh.service
```

修改配置：
```
nano /etc/ssh/sshd_config

PermitRootLogin yes
PasswordAuthentication yes
```


# Debian 软件安装(可选)

[Complex Punk 推荐开发初始化安装套装](./init_setup.md)
