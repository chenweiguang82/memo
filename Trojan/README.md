# 使用Trojan科学上网
自己搭建Trojan其实非常容易，主要需要两个东西
- 1 虚拟主机
- 2 域名

## 虚拟主机
对于虚拟主机，可以自己花钱买，也可以使用免费的AWS，我目前使用的这个，之前的马上到期了，今天又申请了一个，可以继续使用12个月了。
申请免费的AWS需要有可以使用VISA或者MaterCard的信用卡，这个好申请，到时候会扣1USD，过几天就会还回来的。
重点是申请好之后的事情，需要创建一个免费的EC2实例，这里有几个需要注意的地方：
对于Trojan来说，选用Ubuntu就可以了，我选用了20.04。
对于选择在哪个地方建，我选择了日本东京，这个速度还是可以接受的。
对于网络与安全这块，增加对443和80端口的访问，这是HTTPS和HTTP需要的
连接实例是需要使用SSH客户端，增加密钥对，下载下来，使用密钥登录，对于Ubuntu，用户名为ubuntu，我使用的是Xshell，导入密钥就可以登录了。
对于IP地址，对于实例是有一个公有IP和私有IP的，记住公有IP。如果以后公有IP被墙了，到时候可以使用弹性IP再换个IP。
到此为止虚拟主机暂时告一段落

## 域名
对于域名，可以花钱买，也可以申请免费的。 Freenom是可以申请免费1年的，只是初次注册的时候需要提供一个地址信息，可以到网上搜美国地址生成器，可以搞一个虚假地址就行。
之后申请域名，我使用的是ga结尾的，一路下一步就可以申请好。
接下来要对域名进行一些配置，包括DNS服务器和胶水纪录。
DNS服务器可以使用自带也可以使用第三方的，我使用第三方的cloudflare.com，所以需要修改DNS服务器为cloudflare.com的DNS解析服务器
>BURT.NS.CLOUDFLARE.COM
>HARMONY.NS.CLOUDFLARE.COM
胶水记录里可以添加多个二级域名，我使用的就是二级域名，这样可以相当于有多个域名。
Freenom里设置好后到cloudflare.com注册账户，然后把域名加上去，同样在这上面加上胶水记录。这里需要注意的是代理状态选择“仅限DNS”，否则可能域名使用的IP就不是虚拟主机的，而是CDN的。
这里设置后一般需要等一会儿才会生效。

## 安装
上面都结束后就准备好了最开始说的两个东西了，接下来就可以安装了。
登录到服务器，sudo su -切换到root，接下来apt update更新下软件仓库的信息。
然后下载trojan一键安装脚本，这里我使用的是https://v2raytech.com/trojan-one-click-scrip/
使用命令curl -O  https://s.hijk.art/trojan.sh 下载下来，之后chmod +x trojan.sh
接下来./trojan.sh运行脚本按照提示安装即可。

## 客户端
安装后需要本地下载Trojan客户端，我是在这里下载的https://v2raytech.com/trojan-clients/ 配置可以看这里https://v2raytech.com/trojan-windows-client-tutorial/
其实就是修改config.json的local_port, remote_addr和password，local_port默认是1080，我改成1070了，默认不改也可以。remote_addr改成上面的域名，password改成trojan脚本最后生成的。
之后就可以运行trojan.exe了。
