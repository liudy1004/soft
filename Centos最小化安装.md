# [Centos 最小化安装]()

```spreadsheet
// 挂载ISO文件
~]# mount /dev/cdrom /挂载点
```
```spreadsheet
// 编辑YUM仓库
~]# rm -rf /etc/yum.repos.d/*			## 清除多余仓库
~]# vi /etc/yum.repos.d/myrepo.repo
	[myrepo]
	name=centos7.4
	baseurl=file:///挂载点
	enabled=1
	gpgcheck=0
```
```spreadsheet
// 安装常用软件
~]# yum -y install vim-enhanced net-tools wget bash-completion psmisc iproute tree lftp rsync lrzsz scp

    [vim-enhanced]: vim编辑器
    [net-tools]:ifconfig工具
    [wget]:下载工具
    [bash-completion]:tab快捷键(加到解析器的才能用快捷键)
    [psmisc]:ps工具
    [iproute]:路由功能
    [tree]:显示目录
    [lftp]:最小化FTP
    [rsync]:远程同步
    [lrzsz]:window和linux互传
    [scp]:远程同步
```
```spreadsheet
// 网卡
## 新安装的系统,默认的网卡是ens33(举例),而不是eth0.同时没有对应的配置文件,如果不修改网卡名,可以直接添加对应的网卡配置文件.

// 添加网卡
~]# nmcli connection add type ethernet con-name eth0 ifname eth0

// 配置IP地址
~]# nmcli connection modify eth0 ipv4.method manual ipv4.addresses "10.1.1.10/24" ipv4.dns "10.1.1.254" connection.autoconnect yes

// 手动添加配置文件
~]# /etc/sysconfig/network-scripts/
~]# cp ifcfg-lo ifcfg-eth0		## 以lo为模板创建eth0,修改配置即可

// 配置文件
    DEVICE=驱动名称			  ## 就是ifconfig看到的名称
    NAME=显示名称 
    ONBOOT=yes				## 开机启用
    NetworkManager=no		## 不接受NetworkManager控制
    TYPE=Ethernet			## 类型
    BOOTPROTO=static		## 协议static | dhcp | none
    IPADDR=192.168.0.101	## IP地址
    GATEWAY=192.168.0.1		## 网关
    NETMASK=255.255.255.0	## 掩码
    DNS1=202.96.128.166		## vm里面的DNS要指向vm，而不是电信
```
```spreadsheet
// 修改配置文件/etc/default/grup，在[GRUB_CMDLINE_LINUX]最后面加入[net.ifnames=0 biosdevname=0]
~]# vim /etc/default/grup
    ......
    GRUB_CMDLINE_LINUX="crashkernel=auto rhgb quiet net.ifnames=0 biosdevname=0"
    ......
// 执行
~]# grub2-mkconfig -o /etc/grub2.cfg
// 修改网卡配置文件
// 重启reboot
```