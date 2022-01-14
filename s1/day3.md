# 前情回顾：

## 1 栈结构 ：先进后出

​	顺序存储：利用列表进行封装

​	链式存储：利用链表节点，分散存储。

## 2 队列结构：先进先出

​	顺序存储：利用列表 队列封装

​	链式存储 ：利用节点，创建队头队尾变量。



# 树形结构

1对多，要有根。其余节点互不相交 根 子树

![](D:\python 学习笔记\pic\树.jpg)

![](D:\python 学习笔记\pic\树1.jpg)



# 二叉树

每当遍历到没有遍历过的节点时，把它当作新的根来处理，根左右

![](D:\python 学习笔记\pic\二叉树.jpg)

![](D:\python 学习笔记\pic\二叉树1.jpg)

![](D:\python 学习笔记\pic\二叉树2.jpg)

先序遍历：当遍历到没有遍历过的节点时，把它当作新的根来处理，

先序：根左右

中序 左根右

后续，左右根

![](D:\python 学习笔记\pic\先序遍历.jpg)



# 递归函数

直接调用函数本身或间接调用

```
#直接调用
def a()
	a()
	
	间接递归
def a()
	b()
	
def b()
	a()

```

递归函数分2阶段：

递推阶段：从原问题出发，按递推公式从未知推到已知，最终达到递归中止条件

回归阶段：按递归中止条件要求的结果，逆向逐步带入递归公式，回归到原问题的求解。

![](D:\python 学习笔记\pic\递归.jpg)

## 递归优缺点

优点：可以把问题简单化，让思路更为清晰，代码更为简单

缺点：递归因系统环境影响大，当递归深度太多时，可能会得到不可预知的结果

# 二叉树的代码实现

二叉树本身是一种递归结果，可以使用python list进行存储。但如何二叉树的结构比较稀疏的化浪费的空间是比较多的

1. 空节点用Nond表示

2. 飞空二叉树用包含3个元素的列表[d,l,r]表示，起始d表示根节点，l,r左子树和右子树。

   ![](D:\python 学习笔记\pic\二叉树3.jpg)

# 后续 左右根

B F G D I H E C  A

根据后续遍历创建二叉树

```
class Node：
def __init__(self,left,right)
self.left =left
sefl.right = right
#遍历的起始位置 
class Bigtree：
def __init__(self,root)
selt.root =root #-------------传进来谁，谁就是根

class Bitree:
    def __init__(self,root = None ):
        self.root = root
    def preorder(self,node):
       if node is None: ##递归中止条件
           return 'hello'
       print(node.val)#--------------------
       self.preorder(node.left)#---------递归
       self.preorder(node.right)#--------

b =Node（'B')
f =Node('F')
g =Node('G')
d =NOde('D',f,g)
i = Npde('I")
h = Node('H')
e = Node('D',i,h)
c =Node('D',d,e)
a =Node('A',b,c)

```

