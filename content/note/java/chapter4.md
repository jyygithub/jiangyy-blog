---
title: "四、类和对象"
date: 2022-08-04T09:39:18+08:00
draft: false
---

## 类的定义

### 类是对象的模板，对象是类的实例。

### 万物皆是对象。

### 类的基本定义

```java
class Test {

}
```

### 构建类的实例

```java
class Test {

}

class Test1 {
    Test test = new Test();
}
```

## 方法

### 方法是类或对象的行为特征的抽象，方法是类或对象最重要的组成部分。

### 方法不能独立定义，方法只能在类体里定义。

### 永远不能独立执行方法。

```java
class Person {

    String name;

    void say(String sentence) {
        System.out.println(name + "在吟诵：" + sentence);
    }

}

class Test {

    public static void main(String[] args) {
        Person person = new Person();
        person.name = "李白";
        person.say("窗前明月光，疑是地上霜。举头望明月，低头思故乡。");
    }

}
```

## 成员变量和局部变量

### 成员变量指的是在类范围里定义的变量。

### 局部变量指的是在方法里定义的变量。

## 访问控制符

### Java提供了3个访问控制符：private、protected和public

### private：当前类访问权限，只能在当前类的内部被访问。

### default：包访问权限，可以被相同包下的其他类访问。

### protected：子类访问权限，既可以被同一个包中的其他类访问，也可以被不同包中的子类访问。

### public：包访问权限，可以被所有类访问。

## package、import和import static

## 类的继承

### Java的继承通过extends关键字来实现，实现继承的类被称为子类，被继承的类被称为父类（基类、超类）

### 比如：水果和植物，就是继承关系。

```java
class Plant {

    String name;

    void info() {
        System.out.println("我是一种植物，我的名称是：" + name);
    }

}

class Fruit extends Plant {

    @Override
    void info() {
        super.info();
        System.out.println("我是一种植物，也是一种水果，我的名称是：" + name);
    }
}

class Test {

    public static void main(String[] args) {
        Fruit fruit = new Fruit();
        fruit.name = "香蕉";
        fruit.info();
    }

}
```