---
title: "Android发布库到MavenCentral"
date: 2022-08-23T09:43:22+08:00
draft: false
tag : "Maven Central"
---

jCenter不再接受任何新库的提交，Google也已经给出了其官方态度，建议开发者以后发布库都发布到MavenCentral上。

```gradle
pluginManagement {
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
    }
}
```

> 相对于jCenter，MavenCentral的使用显得不那么简单，发布标准、域名限制也是要限制不少。

## 域名准备

加入你要提交一个开源库，引用路径如下：

```gradle
implementation 'com.example:core:1.0.0'
```

那么，你必须要拥有`example.com`这个域名，而这在jCenter那并不做限制。如果你没有域名，也不想花钱，也不是没有办法，我们可以使用Github/Gitee,那么我们引入的路径就成为了：

```gradle
implementation 'io.github.yourusername:core:1.0.0'

implementation 'io.gitee.yourusername:core:1.0.0'
```

## 创建Issue

> Sonatype Issue网址：[https://issues.sonatype.org/](https://issues.sonatype.org/)

### 进入Sonatype Issue网站，创建账号并登录。

| | |
| :---: | --- |
| Email | 邮箱，每次操作，都会收到通知 |
| Full name | 联系人名称 |
| Username | 用户名，也是登录账号，上传代码时会用到 |
| Password | 密码，至少8位，带有大小写字母和字符，上传代码时会用到 |

### 点击新建，创建Issue

| | |
| :---: | --- |
| 项目 | Community Support - Open Source Project Repository Hosting (OSSRH) |
| 问题类型 | New Project |
| 概要 | 可以随便填，或者直接填New Project |
| Group Id | 你的开源库引用路径的Group Id；如果是github项目，就填写io.github.myusername；如果是gitee项目，就填写io.gitee.myusername |
| Project URL | 例如https://github.com/sonatype/nexus-public |
| SCM url | 例如https://github.com/sonatype/nexus-public.git |

## 配置域名

Issue创建成功后，会生成一个类似`OSSRH-XXXXX`的ID，记下这个ID。

如果上一步的Group Id，你选择了github/gitee，那么你只需要在github中创建一个名为`OSSRH-XXXXX`的项目，权限设置为public。

如果您使用了自定义域名的Group Id，那么你需要在域名解析中添加一条记录。

| | | |
| :---: | :---: | :---: |
| 主机记录 | 记录类型 | 记录值 |
| @ | TXT | OSSRH-XXXXX |

域名配置成功后，我们进入创建的问题，添加一条评论`Done`以告诉审核人员就可以了。

接下来就是耐心的等待，一般不会太长，5-10分钟就可以了。审核通过后，我们的Maven仓库就可以使用了。

## 配置签名

> 官方文档：[https://central.sonatype.org/publish/requirements/gpg/](https://central.sonatype.org/publish/requirements/gpg/)

### 下载GPG

在MavenCentral上传的代码都需要GPG签名。下载地址：[http://www.gnupg.org/download/](http://www.gnupg.org/download/)

安装完成后，`gpg --version`查看版本。

### 创建GPG密钥

密钥的创建我们可以采用kleopatra生成，也可以使用命令行生成。我这里记录一下命令行生成过程：

```powershell
$ gpg --gen-key
```

输入名称和邮箱地址
```powershell
Real name: Central Repo Test
Email address: central@example.com
```
输入`O`以确认
```powershell
Change (N)ame, (E)mail, or (O)kay/(Q)uit? O
```
输入8位以上的密码，点击OK即可

{{< figure src="https://s1.ax1x.com/2022/08/24/vc5ZDS.png" >}}

查询所有本地生成的key列表

```powershell
$ gpg --list-keys
C:\Users\Administer\AppData\Roaming\gnupg\pubring.kbx
---------------------------------------------------------
pub   ed25519 2022-08-24 [SC] [expires: 2024-08-23]
      EE230A4B217369C1713B5FF44F6579788EB730F1
uid           [ultimate] Central Repo Test <central@example.com>
sub   cv25519 2022-08-24 [E] [expires: 2024-08-23]
```

### 上传密钥至GPG服务器

```powershell
gpg --keyserver keyserver.ubuntu.com --send-keys EE230A4B217369C1713B5FF44F6579788EB730F1
```

\-\-keyserver指定密钥服务器地址，可选：
- keyserver.ubuntu.com
- keys.openpgp.org
- pgp.mit.edu

\-\-send-keys指定密钥的keyid

### 导出私钥

```powershell
gpg -o D:\secring.gpg --export-secret-keys EE230A4B217369C1713B5FF44F6579788EB730F1
```

## 上传代码

build.gradle

```gradle
plugins {
    id 'com.android.library'
    id 'org.jetbrains.kotlin.android'
    id 'maven-publish'
    id 'signing'
}

publishing {
    publications {
        maven(MavenPublication) {
            afterEvaluate {
                artifact(tasks.getByName("bundleReleaseAar"))
            }
            groupId = 'com.example'
            artifactId = 'core'
            version = '1.0.0'
            pom {
                name = 'core'
                description = 'stydy Mavencentral'
                url = 'https://github.com/example/OSSRH-88888'
                licenses {
                    license {
                        name = 'The Apache Software License, Version 2.0'
                        url = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
                    }
                }
                developers {
                    developer {
                        id = 'YOUR ID'
                        name = 'YOUR NAME'
                        email = 'YOUR EMAIL'
                    }
                }
                scm {
                    connection = 'scm:git@https://github.com/example/OSSRH-88888.git'
                    developerConnection = 'scm:git@https://github.com/example/OSSRH-88888.git'
                    url = 'https://github.com/example/OSSRH-88888'
                }
            }
        }
    }
    repositories {
        maven {
            url 'https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/'
            credentials {
                username = ossrhUsername
                password = ossrhPassword
            }
        }
    }
}

signing {
    sign publishing.publications.maven
}
```

gradle.properties

```properties
signing.keyId=密钥ID
signing.password=密钥密码
signing.secretKeyRingFile=D:\secring.gpg
ossrhUsername=sonatype的用户名
ossrhPassword=sonatype的密码
```

## 发布

进入[https://s01.oss.sonatype.org/](https://s01.oss.sonatype.org/)，账号和密码就是Issue系统的账号密码。

点击左侧的`Staging Repositories`，我们就可以看到我们上传的代码包了。

上方菜单栏共包括五个按钮：Refresh/Close/Promote/Release/Drop。

选中我们上传的代码包，点击`Close`，开始验证代码。

验证完成后，点击`Refrsh`，再点击`Release`即可发布。

发布完成后，我们可以立即在[Sonatype的内容代码库](https://s01.oss.sonatype.org/content/repositories/releases/)看到我们发布的代码库，但是还不能使用依赖引入下载。一般还需要十分钟左右，您的代码版本就会出现在[公开的Maven仓库列表](https://repo1.maven.org/maven2/)，而这时你就可以随意使用了。