---
title: 安装ssh-server
date: 2021-06-16 21:46:36
tags: Ubuntu
categories: OTHER
---

<!-- # 安装 openssh-server -->

一般ubuntu只会安装客户端

```shell
livebug@nuc:~/桌面$ ps -e | grep ssh
   1515 ?        00:00:00 ssh-agent
   3467 ?        00:00:00 sshd
```

## apt-get 安装ssh-server

```shell
livebug@nuc:~/桌面$ sudo apt-get install openssh-server
[sudo] livebug 的密码： 
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
下列软件包是自动安装的并且现在不需要了：
  distro-info
使用'sudo apt autoremove'来卸载它(它们)。
将会同时安装下列软件：
  ncurses-term openssh-sftp-server ssh-import-id
建议安装：
  molly-guard monkeysphere ssh-askpass
下列【新】软件包将被安装：
  ncurses-term openssh-server openssh-sftp-server ssh-import-id
升级了 0 个软件包，新安装了 4 个软件包，要卸载 0 个软件包，有 1 个软件包未被升级。
需要下载 688 kB 的归档。
解压缩后会消耗 6,010 kB 的额外空间。
您希望继续执行吗？ [Y/n] Y
获取:1 http://cn.archive.ubuntu.com/ubuntu focal/main amd64 ncurses-term all 6.2-0ubuntu2 [249 kB]
获取:2 http://cn.archive.ubuntu.com/ubuntu focal-updates/main amd64 openssh-sftp-server amd64 1:8.2p1-4ubuntu0.2 [51.5 kB]
获取:3 http://cn.archive.ubuntu.com/ubuntu focal-updates/main amd64 openssh-server amd64 1:8.2p1-4ubuntu0.2 [377 kB]
获取:4 http://cn.archive.ubuntu.com/ubuntu focal/main amd64 ssh-import-id all 5.10-0ubuntu1 [10.0 kB]
已下载 688 kB，耗时 3秒 (265 kB/s)    
正在预设定软件包 ...
正在选中未选择的软件包 ncurses-term。
(正在读取数据库 ... 系统当前共安装有 162672 个文件和目录。)
准备解压 .../ncurses-term_6.2-0ubuntu2_all.deb  ...
正在解压 ncurses-term (6.2-0ubuntu2) ...
正在选中未选择的软件包 openssh-sftp-server。
准备解压 .../openssh-sftp-server_1%3a8.2p1-4ubuntu0.2_amd64.deb  ...
正在解压 openssh-sftp-server (1:8.2p1-4ubuntu0.2) ...
正在选中未选择的软件包 openssh-server。
准备解压 .../openssh-server_1%3a8.2p1-4ubuntu0.2_amd64.deb  ...
正在解压 openssh-server (1:8.2p1-4ubuntu0.2) ...
正在选中未选择的软件包 ssh-import-id。
准备解压 .../ssh-import-id_5.10-0ubuntu1_all.deb  ...
正在解压 ssh-import-id (5.10-0ubuntu1) ...
正在设置 openssh-sftp-server (1:8.2p1-4ubuntu0.2) ...
正在设置 openssh-server (1:8.2p1-4ubuntu0.2) ...

Creating config file /etc/ssh/sshd_config with new version
Creating SSH2 RSA key; this may take some time ...
3072 SHA256:snuKdsqULYRGawkVjKTyXNxC4YonagqbbkEgZmgHEmc root@nuc (RSA)
Creating SSH2 ECDSA key; this may take some time ...
256 SHA256:B+23mCLgLNM1H2pimspeMd+vZMT/KsxVv1DVq/UuUHc root@nuc (ECDSA)
Creating SSH2 ED25519 key; this may take some time ...
256 SHA256:pn6lQnv8yEwrt/sybmESZMUYRvkwW1Zx1WESMUh3TNk root@nuc (ED25519)
Created symlink /etc/systemd/system/sshd.service → /lib/systemd/system/ssh.service.
Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /lib/systemd/system/ssh.service.
rescue-ssh.target is a disabled or a static unit, not starting it.
正在设置 ssh-import-id (5.10-0ubuntu1) ...
Attempting to convert /etc/ssh/ssh_import_id
正在设置 ncurses-term (6.2-0ubuntu2) ...
正在处理用于 systemd (245.4-4ubuntu3.6) 的触发器 ...
正在处理用于 man-db (2.9.1-1) 的触发器 ...
正在处理用于 ufw (0.36-6) 的触发器 ...
```

## 查看sshd服务状态

```shell
livebug@nuc:~/桌面$ service sshd status
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: e>
     Active: active (running) since Mon 2021-06-14 12:57:59 CST; 3h 43min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 3467 (sshd)
      Tasks: 1 (limit: 38307)
     Memory: 3.0M
     CGroup: /system.slice/ssh.service
             └─3467 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

6月 14 12:57:59 nuc systemd[1]: Starting OpenBSD Secure Shell server...
6月 14 12:57:59 nuc sshd[3467]: Server listening on 0.0.0.0 port 22.
6月 14 12:57:59 nuc sshd[3467]: Server listening on :: port 22.
6月 14 12:57:59 nuc systemd[1]: Started OpenBSD Secure Shell server.
6月 14 13:00:05 nuc sshd[4562]: Accepted password for livebug from 10.42.0.39 p>
6月 14 13:00:05 nuc sshd[4562]: pam_unix(sshd:session): session opened for user>
6月 14 13:00:06 nuc sshd[4658]: Accepted password for livebug from 10.42.0.39 p>
6月 14 13:00:06 nuc sshd[4658]: pam_unix(sshd:session): session opened for user>
```
