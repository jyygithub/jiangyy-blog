---
title: "Gin搭建"
date: 2022-08-12T09:45:07+08:00
draft: false
tag : "Gin"
# cover : "https://avatars.githubusercontent.com/u/7894478"
---
## 环境搭建
### Go安装

```powershell
# Epel安装（可选）
yum install epel-release
# 查询是否有golang
yum search golang
# 安装
yum install golang
# 查看版本
go version
```

### 设置代理

Linux

```powershell
# 设置goproxy.io代理
export GOPROXY=https://goproxy.io
# 设置GO111MOUDLE
export GO111MODULE=on
```

Windows

```powershell
# 注意需要加上引号
# 设置goproxy.io代理
go env -w GOPROXY="https://goproxy.io"
# 设置GO111MOUDLE
go env -w GO111MODULE="on"
```

## Gin开发

```powershell
# 初始化文件夹
go mod init 项目文件名称
# 引入
go get -u github.com/gin-gonic/gin
go get -u gorm.io/gorm
go get -u gorm.io/driver/mysql
```
```go
// 新建main.go文件
package main

import (
	"github.com/gin-gonic/gin"
	"gorm.io/driver/mysql"
	"gorm.io/gorm"
	"net/http"
)

func main() {
	dsn := "username:password@tcp(hostname:port)/databasename"
	db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{})
	if err != nil {
		panic("failed to connect database")
	}

	router := gin.Default()
	v1 := router.Group("/v1")
	{
		v1.GET("/ping", func(c *gin.Context) {
			c.JSON(http.StatusOK, gin.H { "status":1,"data":"success" })
		})
	}
    router.Run() // 默认8080
    // router.Run(":1000")
}
```

## Gin部署
### 编译

```powershell
# 生成二进制文件
go build -o myexe main.go
# 运行即可
./myexe
```

### 部署服务器

```powershell
# 赋予权限
chmod 755 main
# 启动服务
nohup ./main &
```

