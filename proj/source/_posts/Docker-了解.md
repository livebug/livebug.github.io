---
title: Docker 了解
date: 2021-07-13 15:44:23
tags:
- Docker
categories:
- Docker
---
## 安装

[Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

### 遇到的问题

1. Is the docker daemon running?

```shell
$ docker stats
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

需要开启 `docker` 服务.

```shell
$ sudo service docker start
[sudo] password for ubuntu:
 * Starting Docker: docker                                                                         [ OK ]
```

2. `Got permission denied `

```shell
$ docker stats
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/version: dial unix /var/run/docker.sock: connect: permission denied
```

需要修改用户组

```shell
$ sudo groupadd docker
[sudo] password for ubuntu:
groupadd: group 'docker' already exists
$ echo $USER
ubuntu
$ sudo gpasswd -a $USER docker
Adding user ubuntu to group docker
$ newgrp docker
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
