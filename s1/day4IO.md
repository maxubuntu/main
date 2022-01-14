

# day4

## linux一些简要命令

![](D:\python 学习笔记\pic\linux目录结构.jpg)



![](D:\python 学习笔记\pic\常用命令.jpg)

ls - l -a

# IO

在内存中存在数据交换的操作被认为是io操作

程序分类：

​	1.IO密集型程序：在程序中有大量的io操作，而cpu运算较少，消耗cpu少，时间长。

​	2.计算机i密型程序：程序运行中计算较多，IO操作相对较少，cpu消耗多，执行速度块，几乎没有阻塞

文本文件 ：打开后可以自动解码 ：字符串

二进制文件（音频，视频等）：字节串

对于普通的Ascii编码字符串，在前面加B转化为字节串 例如b'hello'

字符串转字节串：str.encode()

字节串转字符串：bytes.decode

s='你好'.encode()



python把文件当作文件对象。

# 文件读写

打开 读写 关闭 三部。

第1步：open()函数

```
file_object = open(file_name,access_mode='r',buffering = -1
功能：打开一个文件，得到一个文件对象
filename ../
r w a r+ W+  ab,rb+ wb+ ab+
```

![](D:\python 学习笔记\pic\fileopen.jpg)

普通文本文件可以既可以用文本方式打开，也可用二进制方式打开

二进制文件则必须以二进制方式打开

![](D:\python 学习笔记\pic\fileopen1.jpg)

2.读写文件按

1. ​	read([size]):

   1. 直接用来读取文中字符

   2. size:给定最多取多少字符。

   3. 文件过大不建议直接读取到文件尾

   4. 读到文件尾会返回空字符串

      ![](D:\python 学习笔记\pic\fileopen2.jpg)

   2.readline([size]):每次读取1行

   ![](D:\python 学习笔记\pic\fileopen3.jpg)

   3.readlines([sizeint]) 读取文中每一行，作为列表中的一项，返回列表

   ```
   date= file1.readlines(18)#前18个字符坐在的行作为读取对象 
   ```

   文件对象本身就是一个可迭代对象

   ```
   for i in file1
   	print i 每次迭代
   	
   ```

   

# 写入文件

writing(string) 文本数据或二进制数据块字符段写入到文件中

参数 需要写入的内容，如果需要换行，自己在内容中添加\n

writelines(str_list):接受一个字符串列表作为参数，将他们写入文件。

参数：要写入的列表





3.关闭文件 file.close()



# 作业

1.熟悉文件的基本操作

2.编写一个文件拷贝程序，要求从终端输入一个文件（可以带路径），将文件保存在当前目录下

​	文件类型不确定。可能文本文件，可能二进制文件

3.编写向一个文件中写日以下内容：

​	1.时间 2019-1-1.。。。 每隔1秒写入1次。

​	2.时间 2019-1-1.。。序号从1排到ctrl-c结束。

​	下次启动程序，要与以前的衔接。



