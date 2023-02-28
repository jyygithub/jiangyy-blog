---
title: "MongoDB安装随笔"
date: 2022-12-23T09:56:54+08:00
draft: false
tag : "MongoDB"
---

## 安装mongoDB

```powershell
$ vim /etc/yum.repos.d/mongodb-org.repo
$ dnf install mongodb-org
$ systemctl enable mongod
$ systemctl status mongod
```
```mongodb-org.repo
[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc
```

## 配置mongoDB

### 权限控制

```powershell
$ vim /etc/mongod.conf
$ systemctl restart mongod
```
```mongod.conf
security:
  authorization: enabled
```

### 用户创建
```shell
$ mongosh
$ use admin
```
```shell
db.createUser(
  {
    user: "mongoAdmin",
    pwd: "changeMe",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```
```shell
$ mongo -u mongoAdmin -p --authenticationDatabase admin
$ use admin
$ show users
```

## 踩坑之路

### 无法再次启动

```shell
Process: ***ExecStart=/usr/bin/mongod $OPTIONS (code=exited, status=14)
```
> 这个问题主要是因为权限不足

```shell
chown -R mongod:mongod /var/lib/mongo
chown -R mongod:mongod /var/log/mongo
chown -R mongod:mongod /tmp/*.sock
```