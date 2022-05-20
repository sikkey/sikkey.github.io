# Debian 用戶管理

# 查看所有用戶

cat /etc/passwd

# 查看某一個用戶

cat /etc/passwd|grep {username}

# 查看用戶組

cat /etc/group

# 查看某一個用戶組

cat /etc/group|grep {groupname}

# Debian 新建用户
linux命令行创建新用户/修改密码/删除用户
```
# cd /usr/sbin
# ./useradd user
# passwd user
# deluser user
```

# 常用

groups 查看當前登錄用戶的額組内成員

groups test 查看test用戶所在的組,以及組内成員

whoami 查看當前用戶名
