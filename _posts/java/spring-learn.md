---
layout: post
title: "Spring的学习使用"
subtitle: "以前写下的对maven配置的记录，迁移到我的新博客"
date: 2019-08-19 22:12:06
author: "Aurora"
tags: java
---

## Spring

总的来说目前我所学习的spring，就是将 bean 对象交给 ApplicationContext.xml 去创建，

{% codeblock ApplicationContext.xml %}
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
</beans>
{% endcodeblock %}

### 手动注入

在 beans 中设置 bean 的属性：
id:指定 bean 的唯一 id
class:指定 bean 绑定的类

bean 的子元素:

<property>:需要 bean 类中有set方法(属性注入(设值注入))
name:绑定 bean 类的属性名,可以使用级联属性赋值
value:设置属性的值
ref:指定引用 bean 的 id
可以在 property 下创建子元素 bean 来创建内部 bean

<constructor-arg>:作用同 property 用于为属性赋值，按 constructor-arg 创建的顺序为 bean 属性赋值，使用以下属性可以更方便的调整设置方法,需要有构造方法(构造注入)
index:可以调整 constructor-arg 的设置顺序
typy:调整 constructor-arg 值的变量类型

## Maven
spring 下 maven 所需要导入的jar包

{% codeblock pom.xml %}
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.1.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.1.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>5.1.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>5.1.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.1.10.RELEASE</version>
    </dependency
{% endcodeblock %}
