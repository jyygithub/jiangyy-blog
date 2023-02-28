---
title: "MySQL安装随笔"
date: 2022-08-12T09:45:04+08:00
draft: false
tag : "MySQL"
---
## 安装MySQL

```powershell
$ wget https://repo.mysql.com//mysql80-community-release-el7-3.noarch.rpm
# 运行以下命令更新YUM源
$ rpm -Uvh https://repo.mysql.com//mysql80-community-release-el7-3.noarch.rpm
# 运行以下命令安装MySQL
$ yum -y install mysql-community-server
# 运行以下命令查看MySQL版本号
$ mysql -V
```

## 配置MySQL
### 启动MySQL

```powershell
# 启动MySQL服务
$ systemctl start mysqld
# 设置MySQL服务开机自启动
$ systemctl enable mysqld
# 运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码
$ grep 'temporary password' /var/log/mysqld.log
```

### 启动后，MySQL会生成一个默认密码

```powershell
$ cat /var/log/mysqld.log | grep password
A temporary password is generated for root@localhost: Qvqs0Pb&widu
```

### 用默认密码即可登录MySQL

```powershell
$ mysql -u root -p
```

### 设置新密码

```powershell
$ ALTER USER USER() IDENTIFIED BY '新密码';

$ ALTER USER '用户登录名'@'localhost'
  IDENTIFIED WITH mysql_native_password
  BY '登录密码';
```

### 授权MySQL远程登录

```powershell
# 查看原有用户
$ use mysql;
$ select user,host from user;
# 查看用户权限
$ show grants for 'root'@'%';
# 新建用户
$ create user '用户登录名'@'%' identified by '用户密码';
# 授权用户（为了安全，仅授权查询权限）
$ GRANT select ON 数据库名.* TO '用户登录名'@'%';
# 撤销授权
$ REVOKE select ON 数据库名.* FROM '用户登录名'@'%' ;
# 刷新权限
$ flush privileges
```

### 查看和修改数据库端口

```powershell
$ show global variables like 'port';
```

### 导入sql文件数据

```powershell
$ create database test;
$ source /root/test.sql
```

## 忘记密码
### 编辑/etc/my.cnf，跳过权限验证

```ini
[mysqld]
skip-grant-tables
```

### 重启mysql

```powershell
systemctl restart mysqld
```

### 操作mysql

```powershell
# 已跳过权限验证，可直接进入
$ mysql
$ use mysql
# 将密码置空
$ update user set authentication_string='' where user='root';
$ flush privileges;
# 删除skip-grant-tables，重启mysql
# 不用输密码即可进入
$ mysql -uroot -p
$ use mysql
# 修改新密码
$ alter user 'root'@'localhost' identified by 'new_password';
$ flush privileges;
```
