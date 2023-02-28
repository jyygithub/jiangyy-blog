---
title: "三、流程控制"
date: 2022-08-03T10:24:26+08:00
draft: false
---
## 顺序机构

程序从上到下逐行地执行

## 分支机构

### if条件语句

```java
if(a > b){

}
```
```java
if (a > b) {

} else {

}
```
```java
if (a > 1) {

} else if (a > 2) {

} else if (a > 3) {

} else {

}
```

### switch分支语句

```java
switch (score) {
    case 'A': {
        System.out.println("优秀");
        break;
    }
    case 'B': {
        System.out.println("良好");
        break;
    }
    case 'C': {
        System.out.println("中");
        break;
    }
    case 'D': {
        System.out.println("及格");
        break;
    }
    default: {
        System.out.println("不及格");
    }
}
```

## 循环机构

### while循环语句

```java
int a = 0;
while (a < 10) {
    System.out.println(a);
    a++;
}
```

### do while循环语句

```java
int a = 0;
do {
    System.out.println(a);
    a++;
} while (a < 10);
```

### for循环

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
```
```java
for (int a = 0, b = 0, c = 0; a < 10 && b < 4 && c < 10; c++) {
    System.out.println(a++);
    System.out.println(++b + c);
}
```

### 嵌套循环

```java
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 5; j++) {
        System.out.println(i + j);
    }
}
```

## 控制循环机构

### 使用break结束循环

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
    if (i == 5) {
        break;
    }
}
```

### 使用continue结束本次循环

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
    if (i == 5) {
        continue;
    }
    System.out.println("continue了哇");
}
```

### 使用return结束方法

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
    if (i == 5) {
        return;
    }
    System.out.println("continue了哇");
}
```

### 与continue和break不同的是，return直接结束整个方法，不管这个return处于多少层循环之内。
