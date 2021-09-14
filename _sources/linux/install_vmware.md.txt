# install centos in vmware

官方安装vmware，

下载centos的iso文件

选择自定义安装

## 选择固件类型

传统BIOS


## 进入自定义设置

处理器和内存

硬盘

## 启动虚拟机


如果有权限提示，记得打开权限允许，否则可能会报错

macos

系统设置 -> 安全与隐私 -> 通用 -> 把vmware的设置放开

## 选择预安装的软件

软件安装：选择最小化，把需要的东西安装即可

安装位置：自动选择

设置root密码

开始安装

## 网络配置

vmware fusion 虚拟机 网络适配器 桥接模式 选择网线或者wifi

选择完之后，重启虚拟机，然后运行

dhclient

来分配一个可用的IP

接下来需要把IP固定下来

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

```
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.2.6
NETMASK=255.255.255.0
GATEWAY=192.168.2.1
DNS1=119.29.29.29
```

编辑完成，重启网络设置即可

centos 7

```
systemctl restart network.service
```


centos 8

```
systemctl start NetworkManager.service 
```