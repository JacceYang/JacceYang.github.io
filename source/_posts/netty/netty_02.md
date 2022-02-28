---
title:  netty 实战入门--系统配置
toc : true
categories:  #分类
    - Netty
tags:   #标签
    - 网络编程
    - Netty
---

这是前言
<!-- more -->
## 系统参数说明



## Linux 系统

### 系统级设置

修改进程级别连接配置

```shell
vim /etc/security/limits.conf

* hard nofile 10000 // * 表示当前用户
* soft nofile 10000
```





### 全局设置

```shell
cat /proc/sys/fs/file-max
```





## Mac 系统

### 操作系统层面的限制

```shell
$ sysctl kern.maxfiles
$ sysctl kern.maxfilesperproc
```



### launchd 对进程的限制

```shell
$ launchtrl limit maxfiles

```



sudo launchctl limit maxfiles 15000 2000000





![image-20211102175131632](/Users/user/Documents/image-20211102175131632.png)



![image-20211102174952277](/Users/user/Documents/image-20211102174952277.png)





![image-20211102200533331](/Users/user/Documents/image-20211102200533331.png)