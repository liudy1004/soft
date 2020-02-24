# [Centos 安装图形界面]()

```spreadsheet
// 安装 x窗口
~]# yum -y groupinstall "X Window System"
~]# yum grouplist
## 安装x窗口后,yum grouplist 查看下"GNOME Desktop"和"Graphical Administration Tools",版本不同显示的名称有所不同.

// 安装图形界面软件
~]# yum -y groupinstall "GNOME Desktop" "Graphical Administration Tools"

// 进入图形界面
~]# startx
```

