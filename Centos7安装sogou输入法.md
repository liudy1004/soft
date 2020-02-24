[TOC]

# [Centos7安装sogou输入法]()

### 本次使用 deb 转 rpm 的方法处理，推荐用第二种方法，perl 编译不懂。



### [一、源码编译]()

下载地址：http://ftp.de.debian.org/debian/pool/main/a/alien/

[ alien_8.87.tar.gz、alien_8.89.tar.gz 随便一个都可以用，这里用8.89版本 ]

```spreadsheet
~]# tar -zxvf alien_8.89.tar.gz
~]# cd alien
~]# perl Makefile.PL
~]# make
~]# make instal
~]# sudo yum -y install qtwebkit
~]# sudo yum -y install fcitx
~]# alien -r sogoupinyin_2.2.0.0108_amd64.deb 
~]# rpm -ivh sogoupinyin_2.2.0.0108_amd64.rpm
~]# reboot
```



### [二、卸载 ibus、安装 fcitx 和 alien]()

```spreadsheet
// 检查ibus是否已安装，有就卸载。
~]# yum list installed | grep -i ibus
~]# yum remove ibus

// 安装fcitx以及依赖包，使用epel源（比较齐全）。
	baseurl=http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/
~]# yum install fcitx fcitx-pinyin fcitx-configtool
~]# yum install *epel*
~]# yum install alien --skip-broken						## 跳过依赖，epel源没有alien其他依赖。
~]# yum install qtwebkit

// alien命令转换rpm。
~]# alien --to-rpm --script  sogoupinyin_2.2.0.0108_amd64.deb 
~]# rpm -ivh --force sogoupinyin-2.2.0.0108-2.x86_64.rpm

// 由于搜狗用的是fcitx，所以要把禁用ibus。这里会报错（没找到，或没权限，不用理会）
~]# gsettings set org.gnome.settings-daemon.plugins.keyboard active false
~]# imsettings-switch fcitx
~]# reboot
```