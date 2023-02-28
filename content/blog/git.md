---
title: "Git的使用指北"
date: 2022-09-03T22:00:39+08:00
draft: false
tag : "Git"
---
> Git官网：[https://git-scm.com/](https://git-scm.com/)

## Git安装

```powershell
yun install -y git

# 查看安装版本
git --version
```

## Git常用命令

```
git init

git add .

git commit -m 'update'

git push

git pull

git clone git@localhost:myname/test.git
```

## 使用SSH密钥

Git远程账户的数据拉去和提交需要进行账户验证，一般包括HTTPS和SSH。

HTTPS方式，使用的仓库地址格式一般为`http://localhost/myname/test.git`，提交/拉取代码时，需要填写用户名和密码。我们可以设置全局用户名和密码，一次设置后可以自动验证，但是由于我们把账号和密码存于本地，会有安全风险。

我们这里使用SSH方式，使用的仓库地址格式一般为`git@localhost:myname/test.git`，提交/拉取代码时，会验证本地SHH密钥。我们在本地生成SSH密钥，把公钥上传至远程Git管理平台，操作代码时，会进行公钥和私钥验证。我们可以随时删除或修改公钥和私钥，所以安全性会比HTTPS验证方式高得多，

### 查看已存在的SSH密钥

```powershell
# ED25519 算法
cat ~/.ssh/id_ed25519.pub

# RSA 算法
cat ~/.ssh/id_rsa.pub
```

### 生成 SSH 密钥

```powershell
# ED25519算法
ssh-keygen -t ed25519 -C "<注释内容>"

# RSA算法
ssh-keygen -t rsa -C "<注释内容>"
```

### 拷贝公钥

```powershell
# windows
cat ~/.ssh/id_ed25519.pub | clip

# macOS
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy

# linux
xclip -sel clip < ~/.ssh/id_ed25519.pub
```