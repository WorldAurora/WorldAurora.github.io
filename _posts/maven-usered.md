---
title: maven的学习使用
date: 2019-09-29 10:38:03
tags: maven
---
本来是想去学习Spring的，但学习Spring需要一点maven的基础，于是决定去学习一下maven，于是在[谷粒学院](http://www.gulixueyuan.com/my/course/42)学习了一下maven

在 [maven官网](https://maven.apache.org/) 根据系统配置好 maven 后就可以使用了

## 结构

以下是一个 maven 的基本目录结构

```
[maven]
--src
----main
------java
------resources
----test
------java
------resources
--pom.xml
```

## pom

pom.xml 的主要内容一般如下

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>[...]</groupId>
	<artifactId>[...]</artifactId>
	<version>[...]</version>
	<name>[...]</name>

	<dependencies>
		<dependency>
			<groupId>[...]</groupId>
			<artifactId>[...]</artifactId>
			<version>[...]</version>
			<scope>[...]</scope>
		</dependency>
	</dependencies>
</project>
```

关于 pom.xml 中选项的解释

groupId: 公司或组织域名倒序+项目名
artifactId: 模块名
version: 版本
scope: 依赖的范围
--compile 主程序 测试程序 打包
--test 测试程序
--provided 主程序 测试程序 (参与开发，但不参与部署，由Servlet容器提供)

## 命令

mvn 的基本命令

```
mvn compile    //编译main目录下的java文件，保存到target目录下
mvn test-compile    //编译test目录下的java文件，保存到target目录下
mvn package    //将maven工程编译为jar包
mvn install    //将当前maven工程的jar包，保存到本地的maven仓库中
mvn clean    //清理编译的target文件
mvn site    //生成站点
```

## Maven jdk版本

找到 mavan 目录下的 settings.xml 文件，往其中添加以下内容

```
<profile>    
    <id>jdk-1.8</id>    
     <activation>    
        <activeByDefault>true</activeByDefault>    
        <jdk>1.8</jdk>    
      </activation>    
    <properties>    
        <maven.compiler.source>1.8</maven.compiler.source>    
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion> 
    </properties>    
</profile>
```
