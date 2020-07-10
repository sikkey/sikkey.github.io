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

安装 ssh (必须先安装client,因为server依赖于client)
```
sudo apt-get install openssh-client openssh-server
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

更多关于 [openssh](./openssh.md) 的用法

安装[vim](./vim.md)，unzip

```
sudo apt-get install vim unzip
```

# xshell 配置退格键

```
会话->属性->终端->键盘
  DELETE 键序列 和 BACKSPACE 键序列
  都设置为 ASCII 127
  保存，重启xshell
```


# Debian 软件安装(可选)

* [openvpn](./openvpn.md)

* [Complex Punk 推荐开发初始化安装套装](./init_setup.md)
