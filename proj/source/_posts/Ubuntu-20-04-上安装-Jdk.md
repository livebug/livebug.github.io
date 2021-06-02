---
title: Ubuntu 20.04 上安装 Jdk
date: 2021-06-02 23:41:26
tags:
- Java
- Ubuntu
categories:
- Java
---
# install java jdk

1. download jdk8 from https://www.jdkdownload.com/
2. unzip and move to `/usr/java`

    sudo mkdir /usr/java/
    sudo tar -zxvf jdk-8u171-linux-x64.tar.gz -C /usr/java/

3. Configure jdk environment variables
    + backup  
        ```
        cp /etc/profile /etc/profile.bak
        ```
    + edit `/etc/profile`
        ```
        export JAVA_HOME=/usr/java/jdk1.8.0_181
        export JRE_HOME=${JAVA_HOME}/jre
        export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
        export PATH=${JAVA_HOME}/bin:$PATH
        ```
    + `/etc/profile` takes effect
        ```
        source /etc/profile
        ```
    + Q: `source /etc/profile` failed  
        edit `/etc/bash.bashrc` ,add JAVA_HOME etc.
        Or  edit `/etc/bash.bashrc`, add `source /etc/profile` 
        Or  edit ` ~/.bashrc`, add `source /etc/profile` 
4. test java env 
```
$ java -version
outpuy: 
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
```
