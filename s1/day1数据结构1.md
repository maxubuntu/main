#day1

# **数据结构**

1. **数据：数据即信息载体,能够被计算机识别，处理，存储的符号总称**

2. **数据元素**

   **数据元素是数据的基本单位，又称为记录，数据由若干基本乡（或称字段，域，属性组成）**

3. **数据结构：指的是由数据元素及元素之间的相互关系，或组织数据的形式**

## **数据之间的结构关系**

1. **逻辑结构**

   **数据之间的抽象关系（如相邻，从属关系），主要分成线性结构和非线性结构两大类**

2. **存储结构**

   **逻辑机构在计算机中具体的实现方法，。**

## **逻辑结构：**

1. **特点：**

   1. **只描述数据结构中数据元素之间的关系**
   2. **是从具体问题中抽象出来的数据模型，**

2. **逻辑机构分类：**

   1. **线性结构 1对1 列表 元组**

      1. **集合中必存唯一的第1个元素**
      2. **集合中必存唯一的最后一个元素**
      3. **除最后个元素外，其他数据元素均为有唯一的后记**
      4. **除第1个元素外，其他的数据元素均为有唯一的前驱**

   2. **树形结构（层次结构 1对多）如公司管理结构 文件的目录**

      1. **每个节点只有1个前驱点**
      2. **每个节点的后续节点可以是多个**

   3. **网状结构 多对多，如高铁，电话线**

      **任意2个节点都可能存在关系**

   **![逻辑结构](D:\python 学习笔记\pic\逻辑结构.jpg)**

   

## **存储结构**

1. **特点：**

   1. **是数据的逻辑结构在计算机存储器的映像或表示（寄存器，主存储器，外存储区）**
   2. **存储结构通过计算机来实现，依赖具体的计算机语言。**

2. **存储分类：**

   1. **存储结构分类**

      1. **顺序存储：将数据结构的各元素按照其逻辑顺序存放在存储器连续的存储空间中**

         1. 特点：读取块，缺点：增删慢

            ![顺序存储](D:\python 学习笔记\pic\顺序存储.jpg)

      2. 链式存储：

         1. 将数据结构中各元素分布在存储器不同点，用记录下一个节点位置的方式建立他们之间的联系。

            1. 特点：增删块，能充分利用内存空间，读取慢,存储 python没有链式存储

               ![](D:\python 学习笔记\pic\链式存储.jpg)

      3. 两者关系

         先考虑什么样的逻辑结构，再考虑用什么存储机构来存，再根据存储结构编写代码来实现

# 线性表模型

​	线性表定义是描述其逻辑结构，通常会在线性表上进行查找 插入	删除等操作

​	线性表作为一种借本的数据结构类型,在计算机存储中的影像（或表示）有2种形式：顺序映像  链式映像

​	列表是线性表种的一种

## 线性表的顺序存储

1. 定义：将线性表L=(a0,a1,a2,a3)中各元素依次存储于计算机一片连续的空间

2. 特点：

   1. 逻辑上相邻的元素如a1.a2,其存储位置也是相邻的
   2. 存储密度高，方便查找
   3. 对表的插入，删除等运算效率较差

3. 程序s实现

   ```
   list01 = [1,2,3,4,5]
   list01.append(10)
   list01.insert
   ```

   

## 线性表的链式存储

1. 定义：将线性表L=(a0,a1,a2..)中个元素分布在存储器的不同储存块，称为节点，每个节点（除尾节点）都持有一个指下一个节点的引用

   ![线性表链式存储](D:\python 学习笔记\pic\线性表链式存储结构.jpg)

2. 特点 

   1. 逻辑上相邻的元素 a1,a2其存储位置不一定相连
   2. 存储稀疏，不开辟整块存储空间
   3. 对表的删除 修改效率高
   4. 逻辑结构复杂 不适合遍历

3. 程序实现

   ```py
   c=3
   b =(2,c)
   a =(1,b)
   print a(1)
   print b(1)
   #可以把a b c看做成在内存中存储的3个节点，每个节点拥有下个节点的引用，可以让上一个节点找到下一个节点，
   ```

   ![](D:\python 学习笔记\pic\线性表链式存储结构1.jpg)



###  创建线性链式存储

​	创建节点类

```py
"""
linklist.py
功能：实现单链列表的勾连和操作
重点代码
"""
#创建节点类
class Node:
"""
    思路：将自定义的类视为节点的生成类，
    实例对象中包含数据类和指向下一个节点的next
    """
    def __init__(self,val, next = None):
        self.val = val #有用数据
        self.next = next #存储下一个节点关系


node1 = Node(1)
node2 = Node(2,node1) #node2.next==node1
node3 = Node(3,node2)#node3.next==node2

a=1
b=(2,a)
c=(3,b)
```



​	[创建自定义节点](D:\pythonstudy\1000课\p2数据结构\day01数据结构\demo1link.py)

![自定义节点类](D:\python 学习笔记\pic\自定义节点类.jpg)	



[线性存储的具体操作](D:\pythonstudy\1000课\p2数据结构\day01数据结构\demo2.py)

​	

# 作业(推荐书：数据结构与算法+python语句描述)

1.对链表进行画图整理

2.编程作业：创建2个链表，两个链表值均为有序值，从小到大，将2个链表合并为1个，合并后要求值认为有序

```
list01=[1,50,100,700]
list02= [2,60,90,700]
```

​	[作业](D:\pythonstudy\1000课\p2数据结构\day01数据结构\d作业.py)



​	



​	



