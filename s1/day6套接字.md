day6

# 回顾

1.读写缓冲区，内存中开辟一块小区域。flush

2.文件偏移量 指定了下1次文件读写的位置 tell() seek()

3.文件处理函数 fileno()

4.网络基本概念理论 

​	*tcp/ip

​	*三次握手 四次挥手过程

​	*tcp udp的理解

概念：ip 域名 端口

5.套接字编程 ：流式 数据报

5 .Tcp服务端

socket---->bind-->listen--->accept---->recv/send---->close

阻塞函数。



# TCP客户端流程

socket-->bind--->connect(可选）---->send/recv---colse

connect

```
cocketfd.connect(server_addr)
功能：连接服务器
参数：元组 服务器地址
```

3 收发消息

注意，防止两端都阻塞，recv send要配合用

## tcp 套接字数据传输特点

1.tcp链接中当1端退出，另1端如果阻塞在recv,此时recv会返回一个空字串

2.tcp连接中如果1端已经不村咋，仍视图通过send发送则会产生brokenPipeErrof

3。一个监听套结字可以同时连多个客户端，也能重复被连接。



# 网络收发缓冲区

1.有效的协调了消息的收发速度

2.send和recv实际是向缓冲区发送接收消息，当缓冲区不为空时，recv就不会阻塞。

![](D:\python 学习笔记\pic\套接字缓冲区.jpg)

# 粘包：

原因：TCP以字节流方式传输，没有消息边界，多次发送的消息被1次接收，此时就会形成粘包

影响：如果每次发送的是一个独立的含义，需要接收端独立解析此时粘包会有影响。

发送接收速率不协调。

处理办法：1.人为添加消息边界

​		  2.控制发放速度



# TCP回顾

1.套接字

服务端流程，客户端流程





# UDP套接字编程

socket---->bind---->recvfrom---->sendto------>close

消息收发： udp不会有粘包

```
data ,addr =sock1.recvfrom(fuffersize)
功能：接收udp消息
参数：每次最多接收多少字节
返回 data发送的内容  bytes格式
	addr 目标地址
n =sock1.sendto(data,addr)
功能 ：发送udp消息
参数：data发送的内容
	addr 目标地址
返回值：发送的字节数
```

D:\pythonstudy\1000课\p4网络编程\day2![](D:\python 学习笔记\pic\套接字2.jpg)

# 套接字属性

```
sockfd.type 套接字类型
sockfd.famely 套接字地址类型
sockfd.getsockname()获取套接字绑定地址
sockdg.fileno()获取套接字文件描述符
sockfd.getpeername()获取连接套接字客户端地址
sockfd.setsockopt(level,option,value)#修改或丰富原套接字的功能
功能：设置套接字选项
level 选项类别 SOL_SOCKET
option 具体选项内容
value 选项值
SO_REUSEADDR :当socket关闭后，本地端用于该socket 的端口号立刻就可以被重用，通常来说，只有警告过系统定义一段时间后才能被重用，布尔型。

sockfd.getsockopt(level,option)
功能：获取套接字选项值
```

```
sock1.setsockopt(socket.SOL_SOCKET,socket.SO_REUSEADDR,1)#设置端口可以立即重用。
```



# UDP的应用

## UDP套接字广播

1.广播定义：一端发送多点接收

2.广播地址：每个网段的最大地址为发送广播的地址，向该地址发送，则网段所有主机都能接收



# TCP套接字之HTTP传输

HTTP协议（超文本传输协议）

1.用途，网页获取，数据传输

2.特点：

​	应用层协议，传输层用tcp传输，

​	简单，灵活，很多语言都有http专门接口

​	无状态，协议不会记录传输内容

​	http1.1支持持久连接，丰富了请求类型

![](D:\python 学习笔记\pic\http应用1.jpg)

![](D:\python 学习笔记\pic\http应用.jpg)



# HTTP请求(request)

## 请求行：具体的请求类别和请求内容

| GET      | /        | HTTP/1.1 |
| -------- | -------- | -------- |
| 请求类别 | 请求内容 | 协议版本 |

请求类别：每个请求表示要做不同的事情。

1. GET:	获取网络资源
2. POST：    提交一定信息，得到反馈
3. HEAD：   只获取网络资源的响应头
4. PUT:           更新服务器资源
5. DELETE：  删除服务器资源
6. CONNECT
7. TRACE:   测试
8. OPTIONS： 获取服务器性能信息

## 请求头：对请求的进一步解释和描述

格式是一个个键值对组成的，每个键值对占1行

accept-Encoding:gzip

## 空行

## 请求体：请求参数或者提交内容

作业：1.熟悉http协议请求格式结构

​	2.熟练四个程序，tcp 2个 udp 2个



