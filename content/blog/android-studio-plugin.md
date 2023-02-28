---
title: "从零开始开发一款JetBrains系插件"
date: 2022-08-16T16:16:47+08:00
draft: false
# cover : "https://s1.ax1x.com/2022/08/16/v0Zy38.png"
tag : "插件开发"
---

## 前言

JetBrains公司开发的IDE全家桶受到了广大开发者的青睐，其强大的插件系统更是在开发中让程序员们如虎添翼，对于插件的开发和上传，JetBrains也开放了入口，并提供了详细的开发文档。

> https://plugins.jetbrains.com/docs/intellij/welcome.html

## 项目新建

JetBrains系列的插件开发，无论我们在实际开发中使用的是IDEA、或者WebStorm、再或是其他的IDE，插件的开发只能使用IDEA，并使用Java或Kotlin进行编写相关代码，这对于我这个Android开发者似乎比较友好，嘻嘻！！

无论是付费的Ultimate版或是免费开源的Community版均可以进行插件开发，所以我选择了Community版的IDEA进行开发（绝不是因为我没钱，嗯……是的）。

IDEA的安装就不讲了，下一步下一步的，无聊的很。安装完IDEA，我们就可以进行项目新建了，这是梦开始的地方。点击`New Project`->`IDE Plugin`，填写完相关信息，点击`create`，我们的项目就新建了。（项目新建后，gradle build，如果是第一次创建，嗯……慢慢等吧。）

- Name：项目名称
- Location：项目路径
- Type：项目类型，这里选择Plguin
- Language：开发语言，可以是Java或Kotlin
- Group、Artifact：这两个的值合并就成为了我们的Plugin ID，例如：com.jiangyy.MyPlugin
- JDK：默认即可，使用Java11。

{{< figure src="https://s1.ax1x.com/2022/09/27/xZ3d9H.png" >}}

## 项目结构

|            ---             | ---                                                          |
| :------------------------: | ------------------------------------------------------------ |
|            目录            | 描述                                                         |
| .gradle、.idea、.run文件夹 | 略。忽视即可，如果使用git进行代码控制，添加到.gitignore。    |
|        gradle文件夹        | gradle的版本文件，默认即可，不用修改。                       |
|         src文件夹          | 我们的代码编写区。                                           |
|      build.gradle.kts      | 项目基本配置，包括应用插件、添加依赖、添加仓库、定义任务等操作。 |
|    gradlew和gradlew.bat    | gradle脚本，默认即可，不用修改。                             |
|        MyPlugin.iml        | 略。忽视即可，如果使用git进行代码控制，添加到.gitignore。    |
|    settings.gradle.kts     | 包含项目间的依赖关系，默认即可，不用修改。                   |

## 插件签名

```powershell
openssl genpkey\
  -aes-256-cbc\
  -algorithm RSA\
  -out private.pem\
  -pkeyopt rsa_keygen_bits:4096
```

```powershell
openssl req\
  -key private.pem\
  -new\
  -x509\
  -days 365\
  -out chain.crt
```

> https://github.com/JetBrains/marketplace-zip-signer

```powershel
java -jar marketplace-zip-signer-cli.jar sign\
  -in "unsigned.zip"\
  -out "signed.zip"\
  -cert-file "/path/to/chain.crt"\
  -key-file "/path/to/private.pem"\
  -key-pass "PRIVATE_KEY_PASSWORD"
```

## 插件发布

- 进入[JetBrans账号中心](https://account.jetbrains.com/)创建JetBrains账号。
- 账号注册后，登录[JetBrains Marketplace](https://plugins.jetbrains.com/author/me)
- 点击右上角账号名称，选择Upload Plugin
- 填写表单相关信息，上传即可。
- 插件上传后，JetBrans官方会在两个工作日内审核完成，然后我们就可以在[插件商店](https://plugins.jetbrains.com/)里搜索到我们的插件了。
