---
title: "使用Docker部署自己的git库"
date: 2022-10-28T14:00:00+08:00
draft: false
tag : "CentOS"
---

## Docker安装

```powershell
yum install -y yum-utils
```

```powershell
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

```powershell
yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## Gitea部署

```powershell
# 拉取最新版Gitea
docker pull gitea/gitea
```

```powershell
# Docker启动
docker run -d --privileged=true --restart=always --name=gitea -p 20022:22 -p 20080:3000 -v /var/lib/gitea:/data gitea/gitea:latest
```

访问http://localhost:20080即可进行gitea配置