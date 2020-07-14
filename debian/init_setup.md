# Complex Punk 推荐开发初始化安装套装

本文随时更新，有时需要清理浏览器缓存后才能刷新

----------

## 配置源
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

## 更新源
```
sudo apt-get update
sudo apt-get upgrade
```

## 安装 openssh
```
sudo apt-get install openssh-server
```

## 安装vim
```
sudo apt-get install vim
```

## 安装跨平台开发环境
```
sudo apt-get install -y build-essential gdb gdbserver rsync
```
启动rsync(一般安装后自动启动),**如果没有rsync, vs2017跨平台开发时无法远程同步源码**
```
rsync --daemon O
```

## 安装源代码版本管理 git
```
sudo apt-get install git
```

## c/c++ 库 (根据项目需要)

### lua
lua json序列化库
```
sudo apt-get install lua-cjson
```

### [zmq](./zmq.md)
