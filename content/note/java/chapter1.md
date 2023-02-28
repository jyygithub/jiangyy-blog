---
title: "一、那些符号"
date: 2022-08-01T10:24:26+08:00
draft: false
---
## 分隔符

### 分号;

在Java中，每个Java语句必须使用分号作为结尾。Java程序允许一行书写多个语句，每个语句之间以分号隔开即可；一个语句也可以跨多行，只要在最后结束的地方使用分号结束即可。

### 花括号\{\}

花括号（{}）的作用为定义一个代码块，代码块在逻辑上是一个整体。

### 方括号[]

方括号（[]）的作用为访问数组元素。

### 圆括号()

圆括号（()）的作用：定义方法时包含所有的形参声明；调用方法时传入实参值；强制类型转换的运算符。

### 空格

空格用于分隔一条语句的不同部分。包含空格符（Space）、制表符（Tab）和回车（Enter）

### 圆点.

圆点：类/对象和它的成员（包括Field、方法和内部类）之间的分隔符

## 标识符

用于给程序中变量、类、方法命名的符号。必须以字母、下划线（\_）、美元符（$）开头，后面可以跟任意数目的字母、数字、下划线（_）和美元符（$）。

## 关键字

### 具有特殊用途的单词

| | | | | | |
| :---: | :---: | :---: | :---: | :---: | :---: |
|abstract|	assert	|boolean|	break|	byte|	case|
|catch|	char|	class|	continue|	default|	do|
|double	|else	|enum	|extends|	final	|finally|
|float|	for|	if|	implements	|import|	int|
|interface|	instanceof|	long|	native|	new|	package|
|private|	protected	|public|	return	|short	|static|
|strictfp	|super|	switch	|synchronized|	this|	throw|
|throws	|transient	|try	|void	|volatile|	while|

## 注释

### 单行注释

### 多行注释

### 文档注释

```java
/**
 * Description:
 * 这是一个Java测试类
 *
 * @author JIANGYY
 * @version 1.0
 */
public class Test {
    /*
     * 这里面的内容就是多行注释
     * 注释对代码执行没有任何改变和影响
     */
    public static void main(String[] args) {
        // 这里执行了一个输出语句
        System.out.println("Hello World!");
        // System.out.println("Hello Java!");
    }
}
```