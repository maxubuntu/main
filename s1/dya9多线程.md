# 创建多线程

![](D:\python 学习笔记\pic\多进程.jpg)

![](D:\python 学习笔记\pic\多进程1.jpg)

![](D:\python 学习笔记\pic\多进程2.jpg)

等同于下面的，更符合面对对象的思想

![](D:\python 学习笔记\pic\多进程3.jpg)

![](D:\python 学习笔记\pic\多进程4.jpg)

多进程中，一般父进程只负责创建子进程，执行子进程，回收子进程，不做别的事，工作都交给子进程做。

![](D:\python 学习笔记\pic\进程9.jpg)

!传递参数

![](D:\python 学习笔记\pic\进程10.jpg)

![](D:\python 学习笔记\pic\进程11.jpg)

![](D:\python 学习笔记\pic\进程12.jpg)

![](D:\python 学习笔记\pic\进程13.jpg)

![](D:\python 学习笔记\pic\进程14.jpg)

![](D:\python 学习笔记\pic\进程16.jpg)

![](D:\python 学习笔记\pic\进程15.jpg)

![](D:\python 学习笔记\pic\进程17.jpg)

p.daemon 是守护进程。

# 守护进程：系统层运行，



​		特点。1.后台运行，与终端无关

​			 2.生命周期长，随操作系统启动而启动，随操作系统终止而终止

​			3.无法在终端对其控制

​		通常用来在后台辅助操作系统的功能



2.通过模块prpcess类创建进程对象，关联函数

3.可以通过进程对象设置进程信息及属性

3.通过进程调用star

# 进程池



![](D:\python 学习笔记\pic\进程18.jpg)

![](D:\python 学习笔记\pic\进程19.jpg)

![](D:\python 学习笔记\pic\进程20.jpg)

![](D:\python 学习笔记\pic\进程21.jpg)

默认参数是你的cpu有几核，就创建几个



![](D:\python 学习笔记\pic\进程22.jpg)

close不能添加新的进程，原有的进程会继续执行。和商店不然进人，但里面的人也不会赶走一样。

![](D:\python 学习笔记\pic\进程23.jpg)

作业 ：1.将聊天室代码梳理一下

​	2.数量multiprocessing模块创建进程

​	3创建2个进程，分别复制一个文件的上下部分，将复制内容放到两个新的文件里面。按字节分文件。





