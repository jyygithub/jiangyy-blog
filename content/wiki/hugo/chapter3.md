---
title: "Hugo的html页面"
date: 2022-08-15T18:11:14+08:00
draft: false
tag : "hugo"
---
## 说在前面的话

> Hugo的文档：[https://gohugo.io/documentation/](https://gohugo.io/documentation/)

我们开始进入主题自定义的实质性阶段，主要是layouts文件夹。

## baseof.html

baseof.html文件是唯一包含所有html元素的文件，也是最像普通html的文件。这个文件中的内容会包含在所有页面中，有点像Java中的基类，所有页面都是继承于这个页面。

统一进行title的声明，所以我们在head加入title，值为`{{ .Title }}`。我们引入这个变量后，每个页面会自动读取每个文件front matter中的title字段。

```html
<title>{{ .Title }}</title>
```

统一引入css，我们不能直接使用相对路径或绝对路径引入，而是要使用`Hugo Pipes`。

```html
<!-- 声明变量，读取css文件 -->
{{ $style_common := resources.Get "css/common.css" | minify | fingerprint }}
<!-- 引入 -->
<link rel='stylesheet' type='text/css' href='{{ $style_common.RelPermalink }}' />
```

我们在body中声明`<div></div>`用来存放主体内容，并分为head和main两个内容块，并命名为：`center_head`和`center_main`。

```html
<div>
    {{ block "center_head" . }}{{ end }}
    {{ block "center_main" . }}{{ end }}
</div>
```

结果例子：

```html
<!DOCTYPE html>
<html lang='zh-CN'>

<head>
    <meta charset='utf-8'>
    <meta name="viewport" content="width=device-width,initial-scale=1.0">

    <title>{{ .Title }}</title>

    <!-- 声明变量，读取css文件 -->
    {{ $style_common := resources.Get "css/common.css" | minify | fingerprint }}
    <!-- 引入 -->
    <link rel='stylesheet' type='text/css' href='{{ $style_common.RelPermalink }}' />

</head>

<body>
    <div>
        {{ block "center_head" . }}{{ end }}
        {{ block "center_main" . }}{{ end }}
    </div>
</body>

</html>
```

## list.html

list.html文件是文章列表页面，hugo会自动解析所有文件夹名称，以显示为列表。如果我们给文章添加了tag、category或者别的集合特征，我们在访问集合特征时也会加载list.html。

例如我们在content文件夹下新建一个study文件夹，我们在访问http://localhost:1313/study时就会自动加载list.html。

因为list.html是继承于baseof.html，所以我们直接使用上面的声明。

使用center_head代码块，这里我们使用`h1`来显示列表名称{{ .Name }}。

```
{{ define "center_head" }}
<header>
    <h1>{{ .Name }}</h1>
</header>
{{ end }}
```

使用center_main代码块，我们需要用循环`range`和页面读取`.Pages`（如果需要分页：可以加`.Paginate`）来显示列表下的文章列表。

```
{{ define "center_main" }}
    {{ $paginator := .Paginate .Pages }}
        {{ range $paginator.Pages }}
            <h2>{{ .Name }}</h2>
        {{ end }}
{{ end }}
```

## single.html

single.html文件是文章内容页面。和list.html一样，是继承于baseof.html，所以我们一样可以使用base.html里的声明。

使用center_head代码块。这里我们使用`h1`来显示文章标题`{{ .Title }}`。

```
{{ define "center_head" }}
<header>
    <h1>{{ .Title }}</h1>
</header>
{{ end }}
```

使用center_main代码块。我们使用`article`显示文章主题内容，文章内容为hugo固定的常量`{{ .Content }}`
```
{{ define "center_main" }}
<article>
    {{ .Content }}
</article>
{{ end }}
```