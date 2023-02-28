---
title: "Hugo环境安装和项目搭建"
date: 2022-08-15T16:18:12+08:00
draft: false
tag : "hugo"
---

## 说在前面的话

一直想搭建一个自己的博客网站，个人域名也是早早就已经拿下。刚开始是打算直接创建动态博客网站，所以使用了[Halo](https://halo.run/)，为此还研究了下docker，最后部署成功了，也确实挺方便的，方便的发布文章，方便的备份网站，不过由于Halo是使用Java开发的，所以对服务器的要求相对高一点，而这让我犹豫了，毕竟俺的小小服务器可不能方这一个项目。当然，动态博客还可以选择[Typecho](https://github.com/typecho/typecho)，以及大名鼎鼎的[WordPress](https://github.com/WordPress/WordPress)，不过，我真的不想那么折腾了，我转而选择了静态网站搭建，毕竟我也没多少文章。

静态网站构建工具那就比较多了，部署也是比较简单，可选择的开源项目也是五花八门。JavaScript开发的[hexo](https://github.com/hexojs/hexo)，Ruby开发的[jekyll](https://github.com/jekyll/jekyll)，Vue驱动的[vuepress](https://github.com/vuejs/vuepress)，当然还有我们的主角Go开发的[hugo](https://gohugo.io/)，最后，我从Github stars、构建速度、上手简易程度、主题自定义成本等多个维度综合考虑，选择了`hugo`。

## Hugo环境配置

> Hugo官网：[https://gohugo.io/](https://gohugo.io/)

`hugo`是基于Go语言开发的静态网站生成器，[官网](https://gohugo.io/)官方说明：`The world’s fastest framework for building websites`。使用了Go语言开发，也使得他的构建速度不容置疑。

hugo的安装也很简单，进入[https://github.com/gohugoio/hugo/releases/](https://github.com/gohugoio/hugo/releases/)下载对应系统的安装包，安装即可。

```powershell
# 验证安装
hugo version
```

## 工具选择

hugo虽然使用Go开发的，不过我们在编写代码时，主要还是HTML和JavaScript开发，所以IDE我们可以优多种选择，这里提供几个选择：jetbrains旗下的[WebStorm](https://www.jetbrains.com/webstorm)、微软开发的[Visual Studio Code](https://code.visualstudio.com/)、国产的[HBuilder X](https://dcloud.io/hbuilderx.html)。

我选择了Visual Studio Code，安装了几个插件：`Better TOML`、`CSS Peek`、`HTML CSS Support`、`Hugo Language and Syntax Support`。配合Git进行版本控制。

## 项目创建

```powershell
hugo new site MyHugo
```
创建的hugo项目会生成以下目录。

- archetypes
- assets：主要存放css/js文件
- content：我们的博客内容，存储markdown文件
- i18n：国际化
- layouts：把markdown文件解析为md文件的模板
- resources
- static：静态文件
- config.toml：配置文件，可以设置toml、taml格式

如果我们使用三方的主题，可以自行创建themes文件夹，复制主题到themes文件夹，在配置项目内声明即可（详细配置主题开发者一般都会说明）。

```powershell
hugo new posts/test.md
hugo server -D
# 打开http://localhost:1313测试
```

## 网站部署

静态网站的部署那时非常简单，甚至很多人使用Github Pages，直接就不需要服务器，直接上传到Github发布就可以访问了，不过因为众所周知的原因，Github的访问速度真的是让人难以忍受，所以，我还是入手了一个小型服务器。

hugo的部署很简单，运行`hugo`命令，生成`public`文件夹，把`public`文件夹的内容复制到服务器，再使用`nginx`代理，轻松完成。
