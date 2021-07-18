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

安装 `docker-compose`

```
$sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-(uname -s)-(uname−s)−(uname -m)" -o /usr/local/bin/docker-compose
$sudo chmod +x /usr/local/bin/docker-compose
$docker-compose --version
```

### 遇到的问题

#### 1. Is the docker daemon running?

```shell
$ docker stats
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

需要开启 `docker` 服务.

```shell
$ sudo service docker start
[sudo] password for ubuntu:
 * Starting Docker: docker                                                               [ OK ]
```

#### 2. Got permission denied

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

#### 3. docker: Error response from daemon:

```shell
$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
docker: Error response from daemon: Head https://registry-1.docker.io/v2/library/hello-world/manifests/latest: read tcp 192.168.31.180:60690->52.55.168.20:443: read: connection reset by peer.
See 'docker run --help'.
```

执行下面命令：

```
sudo systemctl restart docker
```

### CLI 命令说明

#### 1. `docker run -dp 3000:3000 getting-started`

- `-d`:   --detach                         Run container in background and print container ID
- `-p`:   --publish list                   Publish a container's port(s) to the host

#### 2. `docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started`

添加 `-v` 标志来指定卷装载。 你要使用命名卷并将其装载到 `/etc/todos`，这将捕获在该路径中创建的所有文件。
