## 更新源
```
vi /etc/apt/sources.list
```
2020年7月13日 推荐使用buster[清华源](https://mirror.tuna.tsinghua.edu.cn/help/debian/)
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
```

https 上海交大源
```
deb https://mirror.sjtu.edu.cn/debian/ stretch main contrib non-free
deb-src https://mirror.sjtu.edu.cn/debian/ stretch main contrib non-free
deb https://mirror.sjtu.edu.cn/debian/ stretch-updates main contrib non-free
deb-src https://mirror.sjtu.edu.cn/debian/ stretch-updates main contrib non-free
deb https://mirror.sjtu.edu.cn/debian/ stretch-backports main contrib non-free
deb-src https://mirror.sjtu.edu.cn/debian/ stretch-backports main contrib non-free
deb https://mirror.sjtu.edu.cn/debian-security/ stretch/updates main contrib non-free
deb-src https://mirror.sjtu.edu.cn/debian-security/ stretch/updates main contrib non-free
```

debian10 源
```
deb http://deb.debian.org/debian/ buster main contrib non-free
deb-src http://deb.debian.org/debian/ buster main contrib non-free

deb http://deb.debian.org/debian/ buster-updates main contrib non-free
deb-src http://deb.debian.org/debian/ buster-updates main contrib non-free

deb http://security.debian.org/ buster/updates main contrib non-free
deb-src http://security.debian.org/ buster/updates main contrib non-free
```

debian11 源
```
deb http://deb.debian.org/debian/ bullseye main contrib non-free
deb-src http://deb.debian.org/debian/ bullseye main contrib non-free

deb http://deb.debian.org/debian/ bullseye-updates main contrib non-free
deb-src http://deb.debian.org/debian/ bullseye-updates main contrib non-free

deb http://security.debian.org/ bullseye/updates main contrib non-free
deb-src http://security.debian.org/ bullseye/updates main contrib non-free
```

debian12 源
```
deb https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
```

## debian源生成器(暂时不支持新版本)

```
https://debgen.github.io/
```

## 更新软件包索引

```
sudo apt-get update
sudo apt-get upgrade
```

## apt-get 命令教程

```
sudo apt-get update  更新源
sudo apt-get install package 安装包
sudo apt-get remove package 删除包
sudo apt-cache search package 搜索软件包
sudo apt-cache show package  获取包的相关信息，如说明、大小、版本等
sudo apt-get install package --reinstall  重新安装包
sudo apt-get -f install  修复安装
sudo apt-get remove package --purge 删除包，包括配置文件等
sudo apt-get build-dep package 安装相关的编译环境
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
sudo apt-cache depends package 了解使用该包依赖那些包
sudo apt-cache rdepends package 查看该包被哪些包依赖
sudo apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get check 检查是否有损坏的依赖
```

## debian 操作系统升级

### Debian 10 升级至 Debian 12 的詳細指南

#### 重要提醒：

备份数据： 在进行任何系统升级前，務必备份您的重要数据。升级过程中可能发生意外，导致数据丢失。
了解风险： 升级过程可能会遇到问题，如软件包冲突、配置丢失等。请做好心理准备。
选择合适的时间： 选择一个相对空闲的时间进行升级，以免因系统不稳定影响工作。
升级步骤
1. 更新软件源列表:

编辑 /etc/apt/sources.list 文件，将 Debian 10 的源替换为 Debian 12 的源。

```
deb https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src https://ftp.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src https://security.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
```

注意： 备份原有的 /etc/apt/sources.list 文件，以便恢复。

2. 更新 apt:

运行以下命令更新 apt：

```
Bash
sudo apt update
```

請謹慎使用程式碼。

3. 升级系统:

运行以下命令升级系统：

```
Bash
sudo apt dist-upgrade
```

請謹慎使用程式碼。

这个命令会自动处理依赖关系，并升级所有可升级的软件包。

4. 处理冲突和问题:

在升级过程中，可能会遇到一些软件包冲突或配置问题。
仔细阅读终端输出的提示信息，并根据提示进行处理。
如果遇到无法解决的问题，可以尝试搜索相关解决方案，或者寻求社区帮助。

5. 重启系统:

升级完成后，重启系统以使更改生效：

```
Bash
sudo reboot
```

請謹慎使用程式碼。

常见问题与解决方法
软件包冲突:
使用 apt-cache rdepends <package> 检查依赖关系。
手动移除冲突的软件包，或尝试安装不同版本的软件包。
配置丢失:
备份重要的配置文件，例如 /etc/nginx/nginx.conf。
升级完成后，重新配置相关服务。
系统无法启动:
进入恢复模式，尝试修复文件系统。
如果问题严重，可能需要重新安装系统。
其他建议
升级内核: 升级完成后，建议升级内核以获得更好的性能和安全性。
检查系统配置: 升级后，检查系统的各项配置是否正常。
更新第三方软件: 更新从第三方源安装的软件。
注意事项
升级过程可能比较漫长，请耐心等待。
如果您对 Linux 系统不熟悉，建议寻求专业人士的帮助。
参考资料
Debian 官方文档: [已移除無效網址]
温馨提示：

升级前务必做好充分的准备，以免造成不必要的损失。
如果您对升级过程有任何疑问，请随时提出。
免责声明：

本指南仅供参考，不保证升级过程绝对顺利。请您自行承担升级风险。