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

### curl

```
sudo apt-get install curl
```

### lua
安装编译lua必要的库
```
sudo apt-get install libreadline-dev
```
编译lua源码
```
$ mkdir lua_build
$ cd lua_build
$ curl -R -O http://www.lua.org/ftp/lua-5.3.5.tar.gz
$ tar -zxf lua-5.3.5.tar.gz
$ cd lua-5.3.5
$ make linux test
$ sudo make install

cd src && mkdir -p /usr/local/bin /usr/local/include /usr/local/lib /usr/local/man/man1 /usr/local/share/lua/5.3 /usr/local/lib/lua/5.3
cd src && install -p -m 0755 lua luac /usr/local/bin
cd src && install -p -m 0644 lua.h luaconf.h lualib.h lauxlib.h lua.hpp /usr/local/include
cd src && install -p -m 0644 liblua.a /usr/local/lib
cd doc && install -p -m 0644 lua.1 luac.1 /usr/local/man/man1
```
lua json序列化库
```
sudo apt-get install lua-cjson
```

### [zmq](./zmq.md)

### 安裝其他軟體

#### wget (網絡下載)

```
sudo apt-get install wget
```
通過網絡下載文件
```
wget -c ${url}
```

### tar (解壓縮)
壓縮
```
tar -cjf images.tar.bz2 ./images/

tar -zxvf program.tar.gz
```
解壓
```
tar -xjf images.tar.bz2
```

### 安裝

Option 1: dpkg Command

```
sudo dpkg -i <package path>
sudo apt install -f
```

Option 2: apt Package Manager

```
sudo apt install <package path>
```
