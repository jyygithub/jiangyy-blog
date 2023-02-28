---
title: "Hugo的项目目录"
date: 2022-08-15T17:11:14+08:00
draft: false
tag : "hugo"
---

## 说在前面的话

hugo提供了很多[主题模板](https://themes.gohugo.io/)，不少模板也确实比较美观，刚开始我也的确是傻瓜式的选择了一个模板进行了使用，不过在使用过程中总是会遇到不符自己要求的地方，毕竟这是别人开发的主题，和自己的想法总会有出入，所以我选择了自己开发一个主题。为此我查询了大量资料，这里感谢[hugo官方文档](https://gohugo.io/documentation/)，也学习了[Hugo 静态博客建站记](https://zerovip.vercel.app/zh/18284)和[Hugo 不完美教程](https://www.jianshu.com/p/deaa0e58315a)。

## 项目目录介绍

### archetypes

我们在创建完Hugo新项目后，需要创建文章，需要使用命令

```powershell
hugo new 文件夹名/文件名.md
```

生成的文件默认包含了front matter的默认三个字段。这就使用了archetypes里的内容模板，默认包含了一个`default.md`文件。

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: false
---
```

我们新建`archetypes/blog.md`，内容如下。现在使用`hugo new blog/test.md`生成的文章，则是默认包含了以下内容。

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: false
tag : "tag"
---
```

### assets

主要用于存放css/js文件，使用需要`Hugo Pipes`处理。例如，我们要引入highlightjs。

```html
 {{ $style_highlightjs := resources.Get "js/highlight.min.js" | minify | fingerprint }}
<script src="{{ $style_highlightjs.RelPermalink }}"></script>
```

### content

我们的内容文章文件夹

### i18n

国际化

### layouts

Hugo是把我们的markdown文章解析为html页面，而html显示的样式需要我们自定义。`layouts`文件夹就是存储各种html模板文件。

`layouts`文件夹默认包含了：

| | | |
| --- | --- | --- |
| _default | | |
| └──── | baseof.html | 最基础页面 |
| └──── | list.html | 继承于baseof.html，显示文章列表 |
| └──── | single.html | 继承于baseof.html，显示文章详情 |
| 404.html | | 显示404，在nginx配置文件中统一配置 |
| index.html | | 继承于baseof.html，显示主页 |

### resources

### static

静态文件夹，存放图片/文字等内容。hugo生成html文件时，这个文件夹的内容会直接复制到根目录。

### config.yaml

网站配置文件，可以使用toml、yaml和json文件类型，我这里使用了yaml类型。

```yaml
# 隐藏<meta name="generator" content="Hugo 0.101.0">
disableHugoGeneratorInject : true，
# 字数统计包含中文，默认只统计英文
hasCJKLanguage: true
# 网站的链接
baseURL: https://jiangyy.com/
# 网站title
title: 我的网站
# 网站keywords
keywords : 我的网站keywords
# 网站description
description : 我的网站description
# 文章列表分页，每页显示数量
paginate: 10
# 自定义参数
params:
    a: 1
    b: 我的
```

配置文件的参数声明后，hugo会直接引用，我们在layouts文件夹里也可以引用，形式为：`.参数`，首字母大写，用`{{  }}`包裹，例如：
```html
{{ .Title }}
{{ .BaseURL }}
{{ .Params.a }}
```
