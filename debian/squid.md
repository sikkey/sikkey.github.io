# squid

在Debian上安裝和使用Squid

## 安裝

更新軟體包列表：
```
sudo apt update
```

安裝Squid：
```
sudo apt install squid
```

## 使用

啟動Squid：
```
sudo systemctl start squid
```

檢查Squid狀態：
```
sudo systemctl status squid
```

## 配置代理

1. 在瀏覽器中，打開代理設置。
2. 選擇“手動代理配置”。
3. 在“HTTP 主機”字段中，輸入Squid伺服器的IP地址。
4. 在“端口”字段中，輸入Squid的端口號（默認為3128）。
5. 選擇“使用此代理伺服器為所有協議”複選框。
6. 點擊“確定”保存設置。

## 編輯配置文件

Squid的配置文件位於 `/etc/squid/squid.conf` 。您可以使用文本編輯器（例如nano或vim）打開它進行編輯。

### 以下是一些常用的配置選項：

* `http_port` : 指定Squid監聽的端口號。
* `visible_hostname` : 設置Squid伺服器的可見主機名。
* `cache_dir` : 指定緩存目錄的位置。
* `max_obj_size` : 指定最大緩存對象的大小。
* `acl` : 訪問控制列表。

### 示例

以下是一個示例配置文件：
```
http_port 3128
visible_hostname localhost
cache_dir /var/cache/squid
max_obj_size 100 MB

acl localnet src 127.0.0.1/255.0.0.0
acl my_network src 192.168.1.0/24

http_access allow localnet
http_access allow my_network
http_access deny all
```

此配置允許來自本地網路和192.168.1.0/24網段的訪問，並拒絕所有其他訪問。

## 注意事項

Squid默認使用明文代理，因此不建議在公共網路中使用。您可以使用stunnel等工具將Squid配置為使用加密代理。
Squid的配置文件非常複雜，請仔細閱讀文檔再進行編輯。

## 更多信息

Squid官方網站: [https://www.squid-cache.org/](https://www.squid-cache.org/)

# stunnel加密流量

要使用stunnel加密squid代理的流量，您需要在squid和stunnel之間建立一個隧道。

## 步驟

安裝stunnel：
```
sudo apt install stunnel
```

創建stunnel配置文件：
```
sudo nano /etc/stunnel/stunnel.conf
```

在配置文件中添加以下內容：

```
[squid]
client = yes
accept = 127.0.0.1:3128
connect = 8.8.8.8:443
cert = /etc/stunnel/stunnel.pem

[https]
client = no
accept = 443
connect = 8.8.8.8:443
cert = /etc/stunnel/stunnel.pem
```

創建stunnel證書：
```
sudo openssl req -new -x509 -keyout /etc/stunnel/stunnel.pem -out /etc/stunnel/stunnel.pem -days 3650
```

啟動stunnel：
```
sudo systemctl start stunnel
```

配置squid代理：
在squid配置文件 `/etc/squid/squid.conf` 中添加以下內容监听端口：

```
http_port 3128
https_port 443
```

其中，acl代表允许的IP，默认配置中http_access allow localnet被注释了，以至于acl localnet的配置项全部没有启用，无法在局域网访问服务。

```
acl localnet src 10.10.0.0/255.255.255.0
acl localhost src 127.0.0.1/255.255.255.255
...
http_access allow localnet
http_access allow localhost
http_access deny all
```


重啟squid：
```
sudo systemctl restart squid
or
sudo service squid restart
```

## 注意事項

* 您需要將8.8.8.8:443替換為您自己的HTTPS代理伺服器的IP地址和端口號。
* 您需要確保stunnel證書是有效的。
* 默认配置应该删除以下行的注释，启用localnet配置。可以修改acl配置为LAN的网段.
```
http_access allow localnet
```

## squid 服务器操作

```
# 启动
sudo service squid start
# 停止
sudo service squid stop
# 重启
sudo service squid restart
```



## 配置瀏覽器

在瀏覽器中，將代理設置為：

* HTTP代理：127.0.0.1:3128
* HTTPS代理：127.0.0.1:443


## 配置受信

这样配置之后，squid代理服务器就可以使用了，默认的端口是3128，但是为了安全，只让受信的服务器连接，通常还需要对squid配置账号验证授权使用，通过httpd-tools生成密码文件，安装

```
# yum install httpd-tools -y
```

生成密码文件
```
# mkdir /etc/squid3/
# 生成密码文件，指定文件路径，其中squid是用户名
# htpasswd -cd /etc/squid3/passwords squid
#提示输入密码，不能超过8个字符，输入密码123456
测试密码文件

# /usr/lib64/squid/basic_ncsa_auth /etc/squid3/passwords                
squid 123456
OK 
# 测试完成，crtl + c 打断
```

配置squid使用验证，修改配置文件

```
# vim /etc/squid/squid.conf
# And finally deny all other access to this proxy
auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid3/passwords #账户密码文件
auth_param basic realm proxy
auth_param basic children 50 #最多 50 个账户同时运行
auth_param basic realm CoolTube Proxy Server #密码框描述
auth_param basic credentialsttl 2 hours #认证持续时间
acl authenticated proxy_auth REQUIRED #对 authenticated 进行外部认证
http_access allow authenticated #允许 authenticated 中的成员访问
http_access deny all #拒绝所有其他访问
visible_hostname squid.CoolTube #代理机名字

# 这里是端口号，可以按需修改
# http_port 3128 这样写会同时监听 ipv6 和 ipv4 的端口，推荐适应下面的配置方法。
http_port 0.0.0.0:3128
```


初始化服务并重新启动

```
# squid -z
# systemctl restart squid.service
如果开启了防火墙，还要在防火墙中允许端口3128的策略，以CentOS7为例

# 把 3128 端口加入防火墙过滤掉
# firewall-cmd --permanent --zone=public --add-port=3128/tcp
# 重启防火墙
# firewall-cmd --reload
```


如果想新增用户，只需要按照上面的步骤再次生成一次密码文件就可以

## 測試

訪問一個HTTPS網站，檢查是否已加密。

验证步骤

要验证代理是否正常工作，请使用 curl 工具下载网页：

```
# curl -O -L "https://www.redhat.com/index.html" -x "127.0.0.1:3128"
```

如果 curl 没有显示任何错误，并且 index.html 文件可以下载到当前目录中，那么代理工作正常。