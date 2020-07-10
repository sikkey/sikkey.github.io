# OpenVPN Overview
OpenVPN is an SSL/TLS VPN solution. It is able to traverse NAT connections and firewalls. This page explains briefly how to configure a VPN with OpenVPN, from both server-side and client-side.

## Installation
Install the openvpn package on both client and server.
```
# sudo apt-get install openvpn
```
To enable OpenVPN in the Gnome NetworkManager applet for the taskbar notification area, the additional package network-manager-openvpn-gnome has to be installed:

```
# sudo apt-get install network-manager-openvpn-gnome
```
## Configuration
OpenVPN can authenticate users via user/pass, pre-shared key, certificates, etc.
```
sudo openvpn --config client.ovpn
```


## 在客户端上安装OpenVPN
运行以下命令在客户端计算机上安装OpenVPN。
```
# apt-get install openvpn
```
## 使用文本编辑器，设置在“/etc/openvpn/client.conf'OpenVPN的客户端配置，在客户端上。 示例配置如下：
```
script security 3 system
client
remote vpn_server_ip
ca /etc/openvpn/certs/ca.crt
cert /etc/openvpn/certs/client.crt
key /etc/openvpn/certs/client.key
cipher DES-EDE3-CBC
comp-lzo yes
dev tap
proto udp
tls-auth /etc/openvpn/certs/ta.key 1
nobind
auth-nocache
persist-key
persist-tun
user nobody
group nogroup
```
## 运行以下命令将OpenVPN设置为在引导时启动。
```
# update-rc.d -f openvpn defaults
```
## 在客户端上启动OpenVPN服务。
```
# service openvpn restart
```
