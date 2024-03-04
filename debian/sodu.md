# sodu 提权操作

提升{username}权限到sudo list的方法如下：


编辑/etc/sudoers

添加一行 `username ALL=(ALL) ALL   # Change the user name before you issue the commands` 


```bash
su

vim /etc/sudoers

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

{username} ALL=(ALL:ALL) ALL
```


