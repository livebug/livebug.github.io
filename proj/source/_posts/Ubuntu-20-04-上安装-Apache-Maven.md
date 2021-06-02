---
title: Ubuntu 20.04 上安装 Apache Maven
date: 2021-06-02 23:31:55
tags: 
- Ubuntu
- Maven
- Java
categories: 
- Java
---
```
$ sudo apt install maven
$ mvn -version
Apache Maven 3.6.3
Maven home: /usr/share/maven
Java version: 1.8.0_181, vendor: Oracle Corporation, runtime: /usr/java/jdk1.8.0_181/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.8.0-50-generic", arch: "amd64", family: "unix"

```

## Maven 阿里云(Aliyun)仓库
修改 maven 根目录下的 conf 文件夹中的 settings.xml 文件，在 mirrors 节点上，添加内容如下：
```html
<mirrors>
    <mirror>
    <id>aliyunmaven</id>
    <mirrorOf>*</mirrorOf>
    <name>阿里云公共仓库</name>
    <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
</mirrors>
```

# maven 配置指南

打开 maven 的配置文件（ windows 机器一般在 maven 安装目录的 conf/settings.xml ），在<mirrors></mirrors>标签中添加 mirror 子节点:
```XML
<mirror>
<id>aliyunmaven</id>
<mirrorOf>*</mirrorOf>
<name>阿里云公共仓库</name>
<url>https://maven.aliyun.com/repository/public</url>
</mirror>
```
如果想使用其它代理仓库，可在<repositories></repositories>节点中加入对应的仓库使用地址。以使用 spring 代理仓为例：
```XML
<repository>
  <id>spring</id>
  <url>https://maven.aliyun.com/repository/spring</url>
  <releases>
    <enabled>true</enabled>
  </releases>
  <snapshots>
    <enabled>true</enabled>
  </snapshots>
</repository>
```
在你的 pom.xml 文件<denpendencies></denpendencies>节点中加入你要引用的文件信息：
```XML
<dependency>
  <groupId>[GROUP_ID]</groupId>
  <artifactId>[ARTIFACT_ID]</artifactId>
  <version>[VERSION]</version>
</dependency>
```
执行拉取命令：
```sh
mvn install
```