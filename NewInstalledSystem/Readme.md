# 重装系统备忘录
最近一段时间电脑总是正用着突然出现电脑卡顿，半天没反应，甚至蓝屏或者司机，之前从没想到可能是硬盘出问题，直到前两天启动不了了系统，以为系统坏了，就重装了系统，谁知昨天直接就找不到硬盘了，即使进入BIOS里也找不到了，查了下看来很有可能是固态硬盘的掉盘问题，硬盘有问题了。还好在第一次重装系统的时候把数据都移出来了（其实还有个ubuntu，里面也有些文件没有移出来，不过应该不是很重要）。通过京东申请了售后，发现硬盘过了三年质保，没办法只能再买一个了，昨晚下单了一个金士顿的A2000 nvme 500G的，今天送到后开始着手安装。
## Windows 10的安装
首先再msdn.itellyou.cn上下载了最新的win10专业版的iso，然后用老白桃U盘PE系统做了一个系统盘，之后通过PE系统进行了安装。

这里需要注意的地方是对于win10这样的系统，需要一个ESP引导分区，而这个需要分区表从传统的MBR改为GPT。

之后给Windows系统分类300G空间。安装就不细说了，下面说一下安装后做的事情。
### 激活
这里用了一个cmd脚本（MAS_1.0_CRC32_1D90323C.cmd）非常棒，一次就成功了。

### 迅雷
为了快速的下载下面要安装的软件，就先下载了这个。
### WPS
本来我一般是不安装这个的，工作原因，急需，就装了这个校园版，感觉一般用途非常不错，支持国产。
### 微信客户端
工作需要直接就安装了
### Everything
已经是必需品了
### 7-Zip
也已经是必需品了
### Chrome
这个直接下载安装程序然后直接装就可以了，但是奇怪的是每次我安装的都是繁体版本的。

装好后，进入设置-高级-语言-语言-添加语言-中文简体-设为以这种语言显示就可以了。关键是怎么登陆我的Google账户同步之前安装的扩展，关键是SwitchyOmega，用来爬墙。但是这里有一个悖论，登录Google需要爬墙。爬墙现在我用的是Trojan，目前看来还算好，这个目前已经设置好了，关于这个以后有时间再讲，关键是Trojan用的是Socks5代理，Win10系统自带没法设置，需要借助外界的，这里我用的是V2Ray。
#### V2RayN
下载最新版的V2RayN[https://github.com/2dust/v2rayN/releases/download/3.19/v2rayN-Core.zip](https://github.com/2dust/v2rayN/releases/download/3.19/v2rayN-Core.zip),使用V2Ray建立全局Socks5代理。
* 下载后解压缩，然后运行v2rayN.exe
* 选择服务器-添加[Socks]服务器
* 服务器地址填127.0.0.1，服务区端口填1070
* v2rayN图标上点右键-Http代理-选择全局模式
然后就可以爬墙了，这个时候就可以同步Chrome了。

V2rayN的作用也结束了。
#### Xshell，Xshell，Xftp
工作用，看到官网上有测试版，测试版不需要购买，就先用了。

### Office
正式用还得用这个。
这次安装使用了[Office Tool Plus](https://otp.landian.vip/zh-cn/download.html)这个软件，非常不错。
参考这个（[https://www.jianshu.com/p/3d1fffd0bdb2](https://www.jianshu.com/p/3d1fffd0bdb2)）安装教程。
* 选择部署
* 增加产品-选择Office专业增强版2019-批量版
* 语言包为简体中文
* 体系结构：x64-通道：Office2019企业长期版-安装方式：在线安装-安装模块：Office部署工具
* 看到下面又iSlide，以前没用过，搜了下感觉不错，也选上了
#### 开始部署
然后就开始下载安装了，速度很快，应该不到20分钟
之后就可以激活了
#### 激活
* 选择激活
* 选择许可证：ProPlus2019Volume
* 安装许可证
* KMS管理：选择kms.03k.org
* 激活成功
**成功**
### VSC
为了查看一些文本文档，所以安装了这个软件。
但是下载安装后发现界面是英文的。
按照以下办法切换为中文
* Ctrl+Shift+P
* 输入configure display language
* 点击 Add language
* 安装简体中文
* 重启即可
### 百度网盘
为了下载MaterialsStudio
### MaterialsStudio2019
为了构造模型方便
#### 激活
* 安装时候到configure license，勾去掉
* 修改ms2019.lic第一行，替换this_host为计算机名
* 复制许可证文件ms2019.lic到如下路径中（默认路径）
> C:\Program Files (x86)\BIOVIA\LicensePack\Licenses\
> C:\Program Files (x86)\BIOVIA\LicensePack\share\data\
> C:\Program Files (x86)\BIOVIA\LicensePack\win32\bin\


