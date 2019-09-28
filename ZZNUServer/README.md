# RedHat 6.5 升级GLIBC到2.17
最近服务器存储挂了，还没有修好。服务器这样放着浪费，查了下还有一块硬盘一直就没用过，就分区加载了，然后临时用着。

在上面安装了最新的intel编译器，编译了vasp，一切看似没有问题，但是运行的时候发现问题了。
```
/lib64/libc.so.6: version `GLIBC_2.14' not found
```
出现了这样的错误，查了下系统自带的。
```
strings /lib64/libc.so.6|grep GLIBC
```
才发现竟然是2.12版本的。不得不说太老了。

搜了下目前升级GLIBC主要有两种方式：
- 下载glibc源代码编译安装，然后替换原来的
这种风险比较大，很容易出现系统程序崩溃的问题，试了下没敢用。
- 下载适配版本的rpm包
最后找到了，参考这个[帖子](https://www.cnblogs.com/dpf-learn/p/8763696.html)。
```
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-utils-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-static-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-common-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-devel-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-headers-2.17-55.el6.x86_64.rpm &
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/nscd-2.17-55.el6.x86_64.rpm &
```
然后安装
```
sudo rpm -Uvh *-2.17-55.el6.x86_64.rpm --force --nodeps
```
安装后查下发现已经有2.17的了。
** PS: 需要每个节点都安装 **
