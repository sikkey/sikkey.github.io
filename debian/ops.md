# Debian操作系统常用操作指南

## neofetch 查看机器信息

neofetch是一个命令行工具，用于显示系统的操作系统和硬件信息。要安装neofetch，请在终端中运行以下命令：

```bash
sudo apt-get install neofetch
```
查看机器信息

```bash
neofetch
```

## 查看进程的资源占用情况

top命令是一个动态的实时显示系统当前各个进程的资源占用情况的命令。它可以显示系统中消耗资源最多的进程，并且可以根据不同的参数进行排序。

```bash
top
```

查看某个进程的详细信息

```bash
top -p pid
```

根据进程名查找进程

```bash
top -p `pgrep process_name`
```

根据cpu使用率排序

```bash
top -o %CPU
```

根据ram使用率排序

```bash
top -o %MEM
```

根据disk使用率排序

```bash
top -o DISK
```

## 查看进程

```bash
ps -ef
```

查看进程的详细信息

```bash
ps aux
```

## 查看磁盘使用情况

```bash
df -h
```

## 查看内存使用情况

```bash
free -m
```

## systemctl 查看所有服务

```bash
systemctl list-units --type=service
```

## systemctl 查看服务状态

```bash
systemctl status service_name
```

## systemctl 启动服务

```bash
systemctl start service_name
```

## systemctl 停止服务

```bash
systemctl stop service_name
```

## systemctl 重启服务

```bash
systemctl restart service_name
```

## 查看当前文件夹下层的文件大小

```bash
du -ah --max-depth 1
```

## 查看文件夹下所有文件的大小

```bash
du -sh *
```

## 查看文件夹下所有文件的大小并排序

```bash
du -sh * | sort -h
```

## 查看文件夹下的文件信息

```bash
ls -lh
```