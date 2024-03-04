# Debian 操作汇总

[Complex Punk Blog](http://sikkey.github.io/)

# Debian 操作系统的下载与安装

[Debian 官方网站](https://www.debian.org/)

[Debian 10 安装手册](https://www.debian.org/releases/stable/arm64/install.pdf.zh-cn)

[Debian arm 移植](https://www.debian.org/ports/arm/)

[Debian live 映像](https://www.debian.org/CD/live/)   (:-P)类似WINDOWS PE

[Debian 10.4 AMD64 安装映像](http://http.us.debian.org/debian/dists/buster/main/installer-arm64/current/images/)

# putty控制臺 不能删除，删除时出现 退格^H 解決方案

点击上方：文件→属性→终端→键盘，把 delete 和 backspace 序列改为 ASCII 127

# Debian 切换为root用户
```
# su
```
输入命令后提示输入密码，输入密码切换为root用户

# 配置Debian允许root用户登陆GNOME桌面环境

```
1 su
切换为root用户

2 vi /etc/gdm3/daemon.conf
在 security 下面添加 AllowRoot=true
保存后退出vi
3、vi /etc/pam.d/gdm-password

注释掉这一行 auth required pam_succeed_if.so user != root quiet_success
#auth required pam_succeed_if.so user != root quiet_success
保存后退出vi
```

# Debian 新建用户
linux命令行创建新用户/修改密码/删除用户
```
# cd /usr/sbin
# ./useradd user
# passwd user
# deluser user
```

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

# 安装桌面图标功能
```
sudo apt-get install gnome-shell-extension-desktop-icons
```

# Debian 软件安装(可选)

* [openvpn](./openvpn.md)

* [Complex Punk 推荐开发初始化安装套装](./init_setup.md)

* [網路代理squid](./squid.md)

# [Debian操作系统备份与还原](./backup.md)

# Linux中将命令运行结果放到文件中的方法

以ls命令为例

1. 仅转向不显示

（1）ls > test.txt       把输出转向到指定的文件，如文件已存在的话也会重新写入，文件原内容不会保留

（2）ls >> test.txt     是把输出附向到文件的后面，文件原内容会保留下来

2. 转向同时显示

ls | tee ls_tee.txt     把输出转向到指定的文件，同时显示，原文件内容不保存

tee的作用:
　　read from standard input and write to standard output and files
　　它从标准输入读取内容并将其写到标准输出和文件中

3. 同时记录多个命令输出结果

script    启动命令，开始记录

exit      退出命令，结束记录，之所以用exit命令是因为使用script时启动了一个shell，可以通过ps auxfww命令来验证

记录内容默认记录在typescript文件中

script. -a scripttest.txt 指定文件记录命令执行内容
