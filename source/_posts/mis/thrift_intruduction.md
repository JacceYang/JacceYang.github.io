---
title: 了解thrift （一）
toc : true
categories:  #分类
    - Thrift
tags:   #标签
    - RPC
    - Java
---


## thrift 历史

thrift 是由facebook 公司开发的，最初是为了解决不同的跨语言的服务调用。目前支持的语言多达32 种之多。其主不同于以往的大多数网络框架，不仅提供了丰富的数据结构，而且提供了很好的性能。

<!--more-->
## thrift 框架组成
thrift 对软件栈的定义非常清晰。各个组件能够松散的耦合。 正对不同的场景选择不同的方式去搭建服务。


Thrift 栈的模型如下所示：
![image](https://upload.wikimedia.org/wikipedia/commons/d/df/Apache_Thrift_architecture.png)

* 自顶向下分为：服务层（service layer），处理层（Processor layer），协议层（Protocal Layer），（传输层 Transport Layer）.

* 传输层： 负责直接从网络中读取和写入数据，它定义了具体的网络协议，比如说 TCP/IP 传输等

* 协议层：定义了数据传输的格式，负责网络传输数据的序列化和反序列化。比如JSON，XML 和二进制数据等。

* 处理层：处理层由IDL 生成的，封装了具体的底层网络传输和序列化，并委托给用户实现的handler 处理。

* 服务层：整合上述组件，提供具体的网络线程/IO服务模型，形成最终的服务。

## Thrift 特点

**开发速度快**
通过编写RPC接口Thritf IDL文件，利用编译生成器，自动生成服务端 骨架（Skeletons） 和客户端桩 （stubs），从而省去了开发者自定义和维护接口编解码，消息传输，服务器多线程模型等基础工作。

服务端：自需要按照**服务骨架** 即接口，编写好具体的业务处理程序就行了。

客户端：只需要拷贝 IDL定义好的客户端桩和服务对象，然后就可以像本地调用一样调用服务了。

**接口维护简单**
通过维护thrift 格式的IDL文件即可。

**学习成本低**
IDL文件风格类似于 google protobuf，且更加 易读易懂，特别是RPC 服务接口风格，像写一个面向对象的class 一样简单
**跨语言支持**
支持各种语言

**稳定广泛的应用**
目前的使用公司国内外有百度，小米，美团等，稳定高效.

## thrift 支持的数据类型
**基础类型**
bool
byte 
i16
i32
i64
double
string
binary

**结构体类型**
struct 定义的结构体对象

**容器类型**
list
set
map

**异常类型**
Exception 自定义

**服务类型**
service 具体对应的服务类

## Ttransport

* TSocket：使用阻塞式I/O进行传输，是最常见的模式
* TNonblockingTransport：使用非阻塞方式，用于构建异步客户端
* TFramedTransport：使用非阻塞方式，按块的大小进行传输，类似于Java中的NIO

## TPortocal
* Thrift 可以让用户选择客户端和服务端之间的传输通信协议，在传输协议上主要分为 文本和二进制传输协议，而立节约带宽，提高传输效率，一般情况下使用二进制类型的传输协议。目前支持的有如下几种：
* TBinaryProtocal:二进制编码格式进行数据传输
* TCompactProtocal:高效率的、密集的二进制编码格式进行数据传输
* TJSONProtocal:使用JSON文本的数据编码协议进行数据传输
* TSimpleJsonProtocal:：只提供JSON只写的协议，适用于通过脚本语言解析

## 参考文献
https://docs.oracle.com/javase/1.5.0/docs/guide/rmi/spec/rmi-arch2.html