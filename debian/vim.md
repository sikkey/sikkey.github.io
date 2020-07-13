# 副作用
[待解决]debian 10.4 安装vim后，xshell远程无法正常使用退格键，服务器本地terminal也不行

# debian 10.4 install vim

```
# sudo apt-get install vim-common=2:8.0.0197-4+deb9u3
# sudo apt-get install libtinfo5
# sudo apt-get install vim
```
之后退格键失灵

查询后是使用了错误的源(163或者上海交大源，截至2020/7/13存在难以维护的bug)，改用清华源即可.  而且版本也不需要修改

```
# sudo apt-get install vim
```
