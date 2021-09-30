# VM上网--xshell连接

+ 桥接模式--选网卡

+ 找到配置IP地址的文件

  + cd /etc/sysconfig/network-scripts
  + ls
  + vi (打开第一个文件，也就是你主机)
  + 配置
    + IPADDR=
    + NETWASK=
    + GATEWAY=
    + DNS1=
    + DNS2=
    + BOOTPROTO=static
    + ONBOOT=yes
  + 配置完重启网络服务
    + systemctl restart network

  # 连接Xshell

  + 连接时记得关闭防火墙

  + 必须配置这个文件
  + vi /etc/selinux/config
    + SELINUX=disabled





