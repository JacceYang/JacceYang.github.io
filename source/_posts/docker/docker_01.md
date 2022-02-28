---
title:  docker 精通
toc : true
categories:  #分类
    - dokcer
tags:   #标签
    - 容器
    - docker
---


# Docker

## 1、概述

 Docker 解决的是什么问题？

> 项目带上环境一起 打包安装，例如项目带上 mysql，redis ，JDK 等环境。
>
> 项目环境一套可以多处部署，并且保持环境一致

Docker 的思想来自集装箱，各个docker 镜像是独立隔离，不会冲突。

<!-- more -->
## 1.1 历史

2010 年美国一家公司叫做dotCloud 做一些pass 的云计算服务，LXC 有关的容器技术。公司较小，没有钱，如是将代码开源了。开源后不少人发现docker 的优点，如是都过来使用。

2014 年 4月 9日，Docker1.0 发布！



Docker 的火的原因

* Docker 出现之前用的是VM，VM 使用比较耗资源。

* Docker ，镜像十分小，只需做安装最小的包
* 启动很慢



Docker 是Go 语言开发的

Docker 地址：https://docs.docker.com/

Docker 仓库地址：https://hub.docker.com/

**虚拟机技术和容器化技术**

*虚拟化技术*

<img src="/Users/user/Library/Application Support/typora-user-images/image-20211016220952343.png" alt="image-20211016220952343" style="zoom:50%;" />

*容器技术*

<img src="/Users/user/Library/Application Support/typora-user-images/image-20211016220845251.png" alt="image-20211016220845251" style="zoom:50%;" />

**对比**

* 传统虚拟机虚拟出一台硬件，运行一个完整的操作系统，然后在系统上安装和运行让软件
* 容器内的应用直接运行在宿主机内，容器没有自己的内核，也没有虚拟我们的硬件，因此比较轻便
* 每个容器是相互独立的，容器内有自己的文件系统，互不影响
* docker 是用的宿主机的内核，而VM 要单独的用自己的。

**docker 和VM的区别**

![img](/images/docker_vm.png)

**特点**

更高效的计算资源利用



## 2、安装

### 2.1 Docker 架构图

![image-20211016221605043](/Users/user/Library/Application Support/typora-user-images/image-20211016221605043.png)



**镜像**

> 镜像好比一个模板，通过镜像可以产生多个容器实例，例如tomcat 镜像 -> tomcate01 ,tomcate02 .

**容器**



**仓库**

> 存放镜像的地方，分为私有和国外的

### 2.2 安装docker

Mac 下直接去官方地址下载对应的docker 并且安装即可。

* 安装完成后，输入如下：

  ```shell
  >docker -version
  $:Docker version 20.10.8, build 3967b7
  表示安装成功了
  ```

* 查看仓库中有什么镜像没有

  ```dockerfile
  > docker images 
  
  ```

  

* 执行hello-world

  ```shell
  > docker run hello-world
  $: xxxx
  执行成功
  ```

  

 ### 2.3 Hello-World 执行流程

```flow
st=>start: run命令开始
op1=>operation: 本地镜像仓库
op2=>operation: 运行镜像
op3=>operation: 下载远程镜像
cond1=>condition: 本机是否有镜像
cond2=>condition: Docker Hub是否有镜像
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end: 结束框
st(right)->op1(right)->cond1
cond1(yes)->op2(top)
cond1(no)->cond2(right)
cond2(yes)->op3(bottom)
op3(left)->op2(right)
cond2(no)->e
```



### 2.4 docker 工作原理

Docker 是一个CS 结构。docker 的Server 以守护进程的形式运行在主机上，接受来自客户端的请求，并执行客户端的指令。

![image-20211017105418069](/Users/user/Documents/image-20211017105418069.png)

## 3、命令

### 3.0 启动& 关闭 & 重启 docker

```

```



### 3.1 镜像命令

* 镜像查询

```shell
$:docker images [OPTIONS] [REPOSITORY[:TAG]]

# 解释
REPOSITORY：镜像仓库源
TAG  			：镜像TAG
IMAGE ID	： 镜像ID
CREATED 	： 镜像创建时间     
SIZE			： 镜像大小

# 可选项
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
```



* 搜索镜像

```shell
$ docker search

# 解释
NAME 				:
DESCRIPTION  :  
STARS   :
OFFICIAL :  
AUTOMATED: 
# 选项
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
```

* docker pull

  ```
  
  ```

  

* docker rmi 删除镜像

```
$ docker rmi  id # 删除 id 的镜像
$ docker rmi -f id # 强制删除 id 的镜像
$ docker rmi -f $(docker images -aq) # 递归删除所有的镜像
```

### 3.2 镜像命令

```shell
$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# 选项
--name "name" 设置容器的名称
-d  后台方式运行
-it 已交互的形式运行
-p
	 -p ip: 主机端口：容器端口
	 -p 主机端口：容器端口
	 -p 容器端口
-P  随机指定端口
 
 ## 测试进入centos
 $ docker run -it contes
 
 ### 从容器中退出
 $ exit # 退出并关闭容器
 $ Ctl+P+Q # 退出但不关闭容器

 
```

### 3.5 查询运行中的容器

```shell
 ### 查询运行中的容器
 $ docker ps
 
 # 选项
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display container IDs
  -s, --size            Display total file sizes
  
```

### 3.6 删除容器

```shell
$ docker rm 

# 选项
  -f, --force     Force the removal of a running container (uses SIGKILL)
  -l, --link      Remove the specified link
  -v, --volumes   Remove anonymous volumes associated with the container
  
## 操作例子

```

### 3.7 重启容器

```shell
$ docker start  containerId
$ docker restart containerId
$ docker stop containerId
$ docker kill containerId
```

### 3.8 docker 日志



### 3.9 docker inspect

```shell
$ docker inspect containerId

[
    {
        "Id": "20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2",
        "Created": "2021-10-17T06:19:49.3823774Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2387,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-10-17T06:19:49.7494868Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:5d0da3dc976460b72c77d94c8a1ad043720b0416bfc16c52c45d4847e53fadb6",
        "ResolvConfPath": "/var/lib/docker/containers/20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2/hostname",
        "HostsPath": "/var/lib/docker/containers/20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2/hosts",
        "LogPath": "/var/lib/docker/containers/20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2/20bcf3d1ffe6bafa0bc4ca9160e75ef9bde9a0b38c484fc61160612bf3954ce2-json.log",
        "Name": "/laughing_villani",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b337a20709d5f7507a2d7245a534f8148058bc076dc839527d30254d4159870f-init/diff:/var/lib/docker/overlay2/6dbee31889da9df53ce3c63bb479c6345ad9e8ab55603588f91892d9f9efbb36/diff",
                "MergedDir": "/var/lib/docker/overlay2/b337a20709d5f7507a2d7245a534f8148058bc076dc839527d30254d4159870f/merged",
                "UpperDir": "/var/lib/docker/overlay2/b337a20709d5f7507a2d7245a534f8148058bc076dc839527d30254d4159870f/diff",
                "WorkDir": "/var/lib/docker/overlay2/b337a20709d5f7507a2d7245a534f8148058bc076dc839527d30254d4159870f/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "20bcf3d1ffe6",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20210915",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "1490c98a23f546453d3939a641a9debe28af4148fb3cc4ca67c3f3faff9f4621",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/1490c98a23f5",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "d0fe71e7a43950c2874d53a60da45c5199b04f0a181be1a548a664d5133bc817",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "202fdd062e74636d06d79cb468a34cecf26201f1801e77f888f8fd9bb2ffffca",
                    "EndpointID": "d0fe71e7a43950c2874d53a60da45c5199b04f0a181be1a548a664d5133bc817",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```



### 3.10 进入运行的容器

通常容器是以后台方式运行的，需要进入容器，进行一些操作

```shell
$ docker exec -it containerId## 例子$ docker exec -it 20bcf3d1ffe6 /bin/bash
```

* 方式二

  ```shell
  $	docker attach  containerId## 进入容器
  ```

* 区别

  docker exec # 进入容器后开启一个新的终端

  docker attach # 进入容器后不会启动新的终端

### 3.11 copy 文件

```sh
$ docker cp 容器Id：容器内路径  目的主机##$ docker cp 20bcf3d1ffe6:/home/text.java /home
```



![img](/Users/user/Documents/webp.png)



## 作业



安装es

```shell
$ docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag
```



```shell
$ docker run -d --name nginx01 -p 3344:80 nginx
```



## 4、镜像

镜像是一个轻量级的，可执行的独立软件包。docker imags 实际是由一层一层的文件系统组成，这些层级的文件系统是就是UnionFS。

## 5、容器数据卷

mysql 配置 挂载

```shell
$ docker run --name mysql01 -p 3306:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/data -e -MYSQL_ROOT_PASSWORD=123456 -d  mysql:5.7
```

上述命令说明如下：

> --name : 给容器取一个名字
>
> -p ： linux 端口：容器端口映射
>
> **-v : 数据卷的挂载 ， 和 -p 指令类似**
>
> -e : 环境变量设置
>
> **-d : 后台运行 **



**思考问题**

如何对已经启动的容器添加新的挂载点呢？？





### 具名挂载

* 查看挂载

  ```shell
  # 产生一个 具名卷$ docker run -d -P --name nginx01 -v realvolum:/etc/nginx ngnix $ docker volume ls# 查看所有卷的情况DRIVER    VOLUME NAMElocal     0abc83c78f20d6822a478fa6c0bebe80e3e7a63370b501b51122381a824f4b55local     0b3739c79c5afb69d1371a29ef4e8b6d4714d03b8255708ef3f823ba44beb8ablocal     7c01c9b890928c8b033baa84a24640d9b357d75a8d18ce185de957373ccaf46alocal     49ec33b2f27204b831bb3c1672fed668297035493ad98a8ee72874081e443e0dlocal     34856c8fa29f2266d00e13c5efbde38a005acaa94f7084a43e86f603720ebf59local     b807d02a2142773b8f6508c30e010a725b2d444de35451f84fc3dcaa024a92e7local     d78c31fbbc3e7a63937357a0bd38fcb44869c2fb63475de23f2c31304bf8aef3local     realvolum#如上为 具名挂载
  ```

  



### 匿名挂载

```shell
# 产生一个匿名卷$ docker run -d -P --name nginx01 -v /etc/nginx ngnix $ docker volume ls# 查看所有卷的情况DRIVER    VOLUME NAMElocal     0abc83c78f20d6822a478fa6c0bebe80e3e7a63370b501b51122381a824f4b55local     0b3739c79c5afb69d1371a29ef4e8b6d4714d03b8255708ef3f823ba44beb8ablocal     7c01c9b890928c8b033baa84a24640d9b357d75a8d18ce185de957373ccaf46alocal     49ec33b2f27204b831bb3c1672fed668297035493ad98a8ee72874081e443e0dlocal     34856c8fa29f2266d00e13c5efbde38a005acaa94f7084a43e86f603720ebf59local     b807d02a2142773b8f6508c30e010a725b2d444de35451f84fc3dcaa024a92e7local     d78c31fbbc3e7a63937357a0bd38fcb44869c2fb63475de23f2c31304bf8aef3#如上为 匿名卷
```



### 查看具体路径

```shell
$ docker volume inspect d78c31fbbc3e7a63937357a0bd38fcb44869c2fb63475de23f2c31304bf8aef3## 结果[    {        "CreatedAt": "2021-10-23T14:35:35Z",        "Driver": "local",        "Labels": null,        "Mountpoint": "/var/lib/docker/volumes/d78c31fbbc3e7a63937357a0bd38fcb44869c2fb63475de23f2c31304bf8aef3/_data",        "Name": "d78c31fbbc3e7a63937357a0bd38fcb44869c2fb63475de23f2c31304bf8aef3",        "Options": null,        "Scope": "local"    }]
```

**由以上可知，在没有制定卷名的情况下，默认路径在/var/lib/docker/volumes/ 下**



> -v 容器路径   #匿名挂载
>
> -v 卷民：容器 路径  # 具名挂载
>
> -v /宿主机路径 ：容器路径 # 指定挂载
>
> 补充：
>
> $ docker run -d -P --name nginx01 -v /etc/nginx：**ro**  ngnix 
>
> 上面中的 ro 为指读等权限控制



## 6、DockFile

Dockerfile是一个Docker镜像的描述文件，我们可以理解成火箭发射的A、B、C、D…的步骤。Dockerfile其内部**包含了一条条的指令**，**每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建**。如下：

``` shell
$ docker build -f dockerfile1 -t kuangshen/centos .
```



![image-20211024215438844](/Users/user/Documents/image-20211024215438844.png)



```shell
#基于centos镜像FROM centos#维护人的信息MAINTAINER The CentOS Project <303323496@qq.com>#安装httpd软件包RUN yum -y updateRUN yum -y install httpd#开启80端口EXPOSE 80#复制网站首页文件至镜像中web站点下ADD index.html /var/www/html/index.html#复制该脚本至镜像中，并修改其权限ADD run.sh /run.shRUN chmod 775 /run.sh#当启动容器时执行的脚本文件CMD ["/run.sh"]
```

由上可知，Dockerfile结构大致分为四个部分：

　　（1）基础镜像信息

　　（2）维护者信息

　　（3）镜像操作指令

　　（4）容器启动时执行指令



### dockerfile 常用命令







### 新建一个Contenos

```shell
FROM centosMAINTAINER xuanci.xiaohongshu.comENV MY_PAHT /usr/localWORKDIR $MY_PATHRUN yum -y install vimRUN yum -y install net-toolsEXPOSE 80CMD echShell $MY_PATHCMD echo "....end..."CMD /bin/bash
```





### CMD 和 ENTRY POINT 区别

ENTRYPOINT  后面添加的通常是命令追加的形式。



### 制作tomcat

1. 下载tomcat 和JDK 的压缩包

2. 便携式dockerfile

   ```shell
   FROM centos MAINTAINER xuanci.xiaohongshu.comCOPY readme.txt /user/local.readme.txtADD jdk-8suxxx .tar.gz /usr/localADD apache-tomcate .tar.gz /usr/localRUN yum -y install vim 
   ```

   





### docker 镜像发布



docker tag 

docker push





### 数据卷容器

多个容器之间共享数据

```shell
	$ docker run -it --name docker02 --volumes-from docker01 imageId
```



都在本地一个 li b/docker/volums 目录下，

## 7、Dock 网络原理

linux 可以通过 evth-paire 技术 与 docker 内的容器ping 通。docker 在启动的时候，会给他分配的一个网络地址。

docker 多个容器之间也是可以相互ping 通的，在同一个局域网内。

![image-20211024225456597](/Users/user/Documents/image-20211024225456597.png)



## --link

> 原理：在 host 配置中加入了地址映射

### docker network

网络三种模式

bridge 模式

none 模式

host 模式

container 模式

## 8、IDEA 整合Docker

## 9、Dock Compose

## 10、Docker Swarm

