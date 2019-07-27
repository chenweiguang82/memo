# Frp安装配置
实验室有一台服务器，从外网无法直接访问。在外面申请了一个免费12个月的AWS主机，因此打算使用Frp内网穿透使得可以从外面直接访问内网主机。
## Frps 服务端配置
服务端是安装到外网主机上的。外网主机我安装的是ubuntu 18.04。
### 下载可用的Frp程序
```
wget https://github.com/fatedier/frp/releases/download/v0.27.1/frp_0.27.1_linux_amd64.tar.gz
tar xzvf frp_0.27.1_linux_amd64.tar.gz
cd frp_0.27.1_linux_amd64/
```
可以看到有以下几个文件：
```
.
├── LICENSE
├── frpc
├── frpc.ini
├── frpc_full.ini
├── frps
├── frps.ini
├── frps_full.ini
└── systemd
    ├── frpc.service
    ├── frpc@.service
    ├── frps.service
    └── frps@.service
```
其中frps开头的是服务端用，frpc开头的是客户端用(内网主机)。  
把frps复制到`/usr/bin/`下面，frps.ini复制到`/etc/frp/`下，frps.service和frps@.service复制到/lib/systemd/system/下,编辑/etc/frp/frps.ini
```ini
[common]
bind_port = 7000
vhost_http_port = 8001
token = xxxxxxxxxx
```
其中bind_port是用于客户端和服务端进行通信的，vhost_http_port是用于web服务器的（暂时我还没有在内网主机安装，为了以后做准备）,token相当于密码。  
之后把frps.service启用并运行
```
systemctl enable frps.service
systemctl start frps.service
```
这样服务端就配置好了。
## Frp客户端配置
客户端是安装在内网主机上的。内网主机我安装的是Archlinux。安装方法可以使用在服务端一样的方法，不过Archlinux的AUR有更方便的方法。
### 通过AUR安装frpc
```
yay -S frpc
```
这样frpc程序和配置文件ini已经在`/usr/bin/`和`/etc/frp/`下了，frpc.service和frpc@.service也已经在`/usr/lib/systemd/system/`下了。接下来对ini文件进行配置
```ini
[common]
server_addr = x.x.x.x
server_port = 7000
token = xxxxxxxxx

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[web]
type = http
local_port = 8080
custom_domains = www.mydomain.com
```
其中server_addr是服务端ip地址。
配置好之后启用并运行客户端就可以了
```
systemctl enable frpc.service
systemctl start frpc.service
```
接下来就可以使用`ssh -p 6000 服务器ip`，就可以连接内网了。  
使用`http://服务器ip:8001`，就可以连接内网web服务了。
