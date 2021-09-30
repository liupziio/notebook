# 防火墙

使用命令：

查看防火墙状态

```python
systemctl status firewalld.service
```



执行后可以看到绿色字样标注的“active（running）”，说明防火墙是开启状态

关闭运行的防火墙

```python
systemctl stop firewalld.service    
```



如果觉得 每次开机都要关闭防火墙 麻烦那就把防火墙禁用

```python
systemctl disable firewalld.service
```

# MariaDB数据库

```shell
mysql -uroot -p123456
#如果没密码第一次登陆直接-p
```

## 切换操作数据库

```shell
MariaDB [(none)]> use mysql
```

## 查看数据库表

```shell
MariaDB [(mysql)]> select host, user from user;
```

## 更改主机名

```shell
MariaDB [(mysql)]> update user set host='改成什么' where host='被改的';
```

## 重启MariaDB

```shell
[root@server ~]# systemctl restart mariadb
```

## 重启网络服务

```
service network restart
```

## 开启vm出现黑屏解决方案

+ 以管理员身份运行“命令提示符”—> 输入命令：netsh winsock reset —> 运行后重启电脑 —> Enjoy it!
  上述命令作用：重置winsock网络规范