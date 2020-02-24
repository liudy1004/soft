==前言：以下配置和操作仅支持Linux Centos/RedHat。不支持Ubuntu==

# [Centos自定义欢迎界面]()

## **[/etc/issue：登陆系统前显示]()**

```spreadsheet
~]# vim /etc/issue
// 类似"Welcome to -kernel"，后面可以接参数。
\d		## 当前日期
\l		## 虚拟控制台号（相当于 tty0~6）
\m		## 机器类型（相当于 uname -m）
\n		## 主机名（相当于 uname -n）
\o		## 域名
\r		## 内核（相当于 uname -r）
\t		## 当前时间
\s		## 当前操作系统名称
\u		## 当前登录用户的编号
\U		## 显示当前登录用户的编号和用户
\v		## 当前操作系统的版本日期
```



## **[/etc/motd：登陆系统后显示]()**

```spreadsheet
~]# vim /etc/motd
// 根据喜好添加图形或登录语
```
