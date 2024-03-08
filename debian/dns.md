# DNS 服務

主要介紹以下幾款DNS服務
* dnscrypt
* dnsmasq

## dnscrypt 安裝和使用

debian12暂时无法使用
```
apt install dnscrypt
```

去下载dnscrypt 2[安装包](https://github.com/DNSCrypt/dnscrypt-proxy/releases)

### dnscrypt 使用

1. 配置 dnscrypt-proxy
```
sudo vim /etc/dnscrypt-proxy.conf
```

二进制包
```
sudo vim ./dnscrypt-proxy.toml
```


编辑配置文件，设置以下参数：

```
provider: 选择 dnscrypt 服务器提供商
resolvers: 选择要使用的 dnscrypt 服务器
listen_addresses: 设置 dnscrypt-proxy 监听的地址
```

例如：

```
provider=cloudflare
resolvers=1.1.1.1,1.0.0.1
listen_addresses=127.0.0.1:53
```
or
```
server_names = ['cloudflare', 'cloudflare-ipv6']
```



2. 启动 dnscrypt-proxy

```
sudo systemctl start dnscrypt-proxy
```


```
./dnscrypt-proxy -resolve cloudflare-dns.com
```


3. 测试 dnscrypt-proxy

```
nslookup google.com
```

如果查询结果显示使用了 dnscrypt 服务器的 IP 地址，则表示 dnscrypt-proxy 已成功配置并启动。


### 將dnscrypt-proxy可執行文件設置為systemctl啓動

1. 創建 systemd 服務文件

```
sudo nano /etc/systemd/system/dnscrypt.service
```

**2. 在服務文件中添加以下內容：

```
[Unit]
Description=DNSCrypt Service

[Service]
Type=simple
ExecStart=/path/to/dnscrypt
Restart=always

[Install]
WantedBy=multi-user.target
```

3. 替換 /path/to/dnscrypt 佔位符

```
sudo vim /path/to/dnscrypt.toml
```

4. 在配置文件中添加以下內容：

```
listen_address = ['127.0.0.1:5333']
```

5. 重新加載 systemd 服務配置：

```
sudo systemctl daemon-reload
```

6. 啟用服務：

```
sudo systemctl enable dnscrypt.service
```

7. 啟動服務：

```
sudo systemctl start dnscrypt.service
```

8. 驗證 dnscrypt 是否正在運行：

```
sudo systemctl status dnscrypt.service
```

## dnsmasq 安裝和使用

### dnsmasq 安装

1. 安装 dnsmasq
```
sudo apt install dnsmasq
```

### dnsmasq 使用

dnsmasq 的默認端口是 53。您可以通過以下方法更改 dnsmasq 的端口：

* 打開 dnsmasq 的配置文件。默認情況下，該文件位於 /etc/dnsmasq.conf。
* 找到以下行：
```
port=53
```

* 將該行更改為以下內容(一般不建議修改)：
```
port=<new_port>
```

* 保存配置文件。
* 重啟 dnsmasq。

1. 配置 dnsmasq
```
sudo vim /etc/dnsmasq.conf
```

编辑配置文件，设置以下参数：

```
listen-address: 设置 dnsmasq 监听的地址
domain: 设置本地域名
dhcp-range: 设置 DHCP 服务的 IP 地址范围
```

例如：

```
listen-address=127.0.0.1
domain=localdomain
dhcp-range=192.168.1.100,192.168.1.200
```

2. 启动 dnsmasq

```
sudo systemctl start dnsmasq
```

3. 测试 dnsmasq

```
nslookup localhost
```

如果查询结果显示了本地域名的 IP 地址，则表示 dnsmasq 已成功配置并启动。

### dnsmasq 快捷安裝

```
sudo apt install dnsmasq
sudo vim /etc/dnsmasq.conf
```

edit dnsmasq.conf

```
port = 53
no-resolv
server=127.0.0.1#5333
server=/localnet/127.0.0.1#5333
server=/cn/114.114.114.114
```

edit /etc/hosts

```
sudo vim /etc/hosts

<add line>
192.168.0.XXX gateway.local
```


```
sudo systemctl restart dnsmasq
```

測試

```
nslookup www.google.com
nslookup www.google.com 127.0.0.1
nslookup gateway.local 127.0.0.1
```


# 配置DNS


配置/etc/resolv.conf 

```
vim /etc/resolv.conf 
```

/etc/resolv.conf 文件是 Linux 系統的 DNS 解析器配置文件。它用於指定本機使用的 DNS 服務器的 IP 地址。

/etc/resolv.conf 文件的格式非常簡單，每行以一個關鍵字開頭，後跟一個或多個由空格隔開的參數。

以下是一些常用的關鍵字和參數：

nameserver：指定 DNS 服務器的 IP 地址。
search：指定搜索域名。
domain：指定默認域名。
options：指定 DNS 解析器的選項。
以下是一個示例 /etc/resolv.conf 文件：

```
nameserver 192.168.0.200
search localdomain example.com
domain localdomain
options edns0
```

該文件配置了以下內容：

使用 IP 地址為 192.168.0.200 的 DNS 服務器解析域名。
搜索域名 localdomain 和 example.com。
默認域名為 localdomain。
啟用 EDNS0 擴展。
您可以使用以下方法為 /etc/resolv.conf 文件添加註釋：

在行首添加井號 (#)。
在行尾添加註釋文字。
以下是一個示例：

```
# 使用 IP 地址為 192.168.0.200 的 DNS 服務器解析域名
nameserver 192.168.0.200

# 搜索域名 localdomain 和 example.com
search localdomain example.com

# 默認域名為 localdomain
domain localdomain

# 啟用 EDNS0 擴展
options edns0
```

添加註釋可以幫助您理解 /etc/resolv.conf 文件的配置。

以下是一些有關如何注釋 /etc/resolv.conf 文件的建議：

對每個關鍵字和參數添加簡要的說明。
解釋任何複雜的配置。
記錄您對配置文件所做的任何更改。

```
# 使用 IP 地址為 192.168.0.200 的 DNS 服務器解析域名
# nameserver 192.168.0.200

# dnscrypt
# nameserver 127.0.0.1:53

# dnsmasq
nameserver 127.0.0.1:5353
```


