# 																																																																																																																																																																		day1 day2小结

##.线性链式存储的操作

```py
#创建节点类
class Node:
    """
    思路：将自定义的类视为节点的生成类，
    实例对象中包含数据类和指向下一个节点的next
    """
    def __init__(self,val, next = None):
        self.val = val #有用数据
        self.next = next #存储下一个节点关系

#链表操作
class LinkList:
    """
    单链表：线性结构链式存储的简称
    生成对象可以进行增删改查操作
    具体操作同过调用具体方法完成
    """
    def __init__(self):
        """
        初始化链表，标记一个链表的开端，便于获取后续的节点
        """
        self.head = Node(None)
    #通过list1为链表增加1组新节点
    def int_list(self,lst):
        p = self.head
        for item in lst:
            p.next =Node(item)
            p = p.next

    #遍历列表
    def show(self):
        p =self.head.next #第1个节点
        while p is not None:
            # print(p)
            print(p.val)
            p = p.next #节点往后移动

    #判断链表为空
    def is_empty(self):
        if self.head.next is None:
            return True
        else:
            return False

    #清空列表
    def clear(self):
        self.head.next = None

    #在尾部插入
    def append(self,val):
        """
        尾部插入
        :param val: 插入的元素
        :return:
        """
        p = self.head
        while p.next is not None:
            p = p.next
        p.next = Node(val)

    #头部插入
    def insert_head(self,value):
        """
        列表头部插入
        :param value: 插入的元素
        :return:
        """
        node =Node(value)
        node.next =self.head.next
        self.head.next = node

    #中间插入
    def insert_midle(self,index,value):
        """
        列表中间插入
        :param index: 索引
        :param value: 插入的元素
        :return:
        """
        node = Node(value)
        p = self.head
        count = 0
        #找到插入点前一个节点
        while count <index:
            if p.next is not None:#判断是否超范围
                p =p.next
                count +=1
            else:
                break

        node.next = p.next
        p.next = node

    #按索引删除节点
    def delete_index(self,index):
        """
        按索引删除元素
        :param index: 索引
        :return:
        """
        p = self.head
        for i in range(index):
            if p.next is None:
                return '炒索引范围'
            p = p.next
        node = p.next.next
        p.next = node

    # 按元素名称删除第1个节点
    def remove(self, value):
        """
        按元素名称删除元素
        :param value: 预删除的元素值
        :return:
        """
        p = self.head
        while p.next and p.next.val == value:##p.next需要放前面，先判定是否到尾部，再判定是否有相同值
            p = p.next
        if p.next is None:#判断到底是哪个条件结束
            raise ValueError('该元素不存在')
        node = p.next.next
        p.next = node

    #获取节点元素
    def find(self,index):
        """
        按索引获取元素值
        :param index: 索引
        :return:返回获取元素值
        """
        p = self.head
        for i in range(index):
            if p.next is None:
                raise '索引错误'
            p = p.next
        return p.val

```

##.栈的顺序操作（入栈，出栈，判断列表是否为空，查看栈顶元素。

1. 栈：栈是限制在一端进行插入操作和删除操作的线性表，允许进项操作的一段称为‘栈顶’，另1端称为‘栈底’，当栈中没有元素时称‘空栈’
2. 特点
   1. 栈只能在一端进行数据操作
   2. 栈模具有先进后出，有进先处的规律

```
class StackError(Exception):
    pass

#顺序栈类

class Sstack:
    def __init__(self):
        #空列表就是栈的存储空间，列表太灵活，要加以限制
        #列表的最后一个元素作为栈顶。
        self._elems = []
        # 判断列表是否空
    def is_empty(self):
        return self._elems == []

    #入栈：
    def push(self,val):
        self._elems.append(val)
    #出栈：
    def pop(self):
        if self.is_empty():
            raise StackError()
        return  self._elems.pop()
    #查看栈定元素
    def top(self):
        if self.is_empty():
            raise  StackError('stack is empty')
        return self._elems[-1]
```

##.栈的链式操作：

```
思路分析：
1.源于链列表结构，
2.封装栈的操作方法（入栈出栈栈空，找定元素）
3.链表开头作为栈顶。（不用每次遍历）

class Node:
    """
    思路：将自定义的类视为节点的生成类，
    实例对象中包含数据类和指向下一个节点的next
    """
    def __init__(self,val, next = None):
        self.val = val #有用数据
        self.next = next #存储下一个节点关系

class Lstack:
    """
    单链表：线性结构链式存储的简称
    生成对象可以进行增删改查操作
    具体操作同过调用具体方法完成
    """
    def __init__(self):
        # 标记栈点位置
        self._top = None
        #栈点是否为空

    def is_empyt(self):
        return self.top is None

    def push(self,val):
        self._top = Node(val,self._top)

    def pop(self):
        if self.is_empyt():
            raise StackError('stack is empty')
        else:
            value= self._top.val
            self._top =self._top.next
            return value
    def top(self):
        if self.is_empyt():
            raise StackError('stack is empty')
        else:
            return self._top.val
```

#.队列

1.队列限定在两端进行插入操作和删除操作的线性表，允许进行存入操作的一端称对尾，允许进行删除操作的一段称对头

上车 吃饭 数学模型

2.特点 

​	。队列只能看到对头和队尾进行数学操作

```
"""
自定义队列
循环出队入栈
循环出栈入队

"""

"""
自定义队列异常
思路分析：
1.基于列表完成数据存储
2.通过封装规定数据操作
3.先确定列表的哪段作为队头和队尾

"""
class QueueError(Exception):
    pass

#队列操作
class Squeue:
    def __init__(self):
        self._element = []

#是否为空
    def is_empty(self):
        return self._element == []
#入队
    def ensqueue(self,value):
        self._element.insert(0,value)
#出队
    def dequeue(self):
        if self.is_empty():
            raise Squeue('队列异常')
        return self._element.pop()

```

链式队列

```
"""链式队列
重点代码
思路
1.基于链表构建队列模型
2.链表的开端最为队头，结尾作为队尾
3.单独定义队尾标记，避免次插入重新遍历
4.当队头和队尾重叠的时候认为队列为空。
"""
class QueueError(Exception):
    pass

class Node:
    """
    思路：将自定义的类视为节点的生成类，
    实例对象中包含数据类和指向下一个节点的next
    """
    def __init__(self,val, next = None):
        self.val = val #有用数据
        self.next = next #存储下一个节点关系

#实现队列操作
class LQueue:
    def __init__(self):
        #定义队头和尾的变量
        self.front = self.rear =Node(None)
    def is_empty(self):
        return  self.front == self.rear

    #入队 rear动
    def enqueue(self,val):
        self.rear.next =Node(val)
        self.rear = self.rear.next
    #出队 front动 front指向谁 谁就已经出队了
    def dequeue(self):
        if self.front == self.rear:
            raise  QueueError('empty in queue')
        self.front =self.front.next
        return self.front.val
```

