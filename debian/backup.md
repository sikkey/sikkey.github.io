# 操作系统备份与还原

## 备份
```
# tar -cvpzf /home/user/Backup/backup.tgz --exclude=/proc --exclude=/lost+found --exclude=/home --exclude=/mnt --exclude=/media /
```

## 还原
```
# tar -xvpzf /home/user/Backup/backup.tgz -C /
```
