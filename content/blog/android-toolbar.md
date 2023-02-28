---
title: "Android自定义View：Toolbar"
date: 2022-08-19T11:26:09+08:00
draft: true
tag: Android
---

## 前言

在实际开发中，我们常会用到工具栏Toolbar。Android官方给我们提供了官方控件：`androidx.appcompat.widget.Toolbar`，设计风格使用Design风格设计，功能也是不少，不过在实际项目中，总是会和UI设计有点误差，所以我们还是自己定义一个Toolbar吧。

开始前可以看看[androidx.appcompat.widget.Toolbar的源代码](https://cs.android.com/androidx/platform/frameworks/support/+/androidx-main:appcompat/appcompat/src/main/java/androidx/appcompat/widget/Toolbar.java)

{{< figure src="https://img-blog.csdnimg.cn/e3cbf1645ec040179510374460a97c7f.png" >}}

## 功能设计

| | | |
| :---: | :---: | :---: |
| | 类型 | 位置 |
| 标题 | 文字 or 图标 | 居中、左对齐、右对齐 |
| 左按钮 | 文字 or 图标 or 图文 | 左对齐 |
| 右按钮 | 文字 or 图标 or 图文 | 右对齐 |

## 代码设计

### 自定义ViewGroup

由于Toolbar需要包含多个控件，所以我们直接自定义ViewGroup。默认的style我们可以使用androidx.appcompat.R.attr.toolbarStyle

```kotlin
class Toolbar : ViewGroup {
    constructor(context: Context) : this(context, null)
    constructor(context: Context, attrs: AttributeSet?) : 
        this(context, attrs, androidx.appcompat.R.attr.toolbarStyle)
    constructor(context: Context, attrs: AttributeSet?, defStyleAttr: Int) : 
        super(context, attrs, defStyleAttr) {
            // TODO
        }
}
```

### 控件定义

```kotlin
private var mTitleTextView: TextView? = null

private var mStartTextView: TextView? = null
private var mStartImageView: ImageView? = null

private var mEndTextView: TextView? = null
private var mEndImageView: ImageView? = null

fun setTitle(title: CharSequence?) {
    // TODO
}

fun setStart(startIcon: Drawable?, startText: CharSequence?) {
    // TODO
}

fun setEnd(endIcon: Drawable?, endText: CharSequence?) {
    // TODO
}
```

## 使用

```xml
<com.jiangyy.widget.Toolbar
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:endText="@string/app_name"
    app:startIcon="@drawable/ic_baseline_arrow_back_24"
    app:title="测试标题"
    app:titleGravity="start"
    app:titleTextColor="@color/white"/>
```
