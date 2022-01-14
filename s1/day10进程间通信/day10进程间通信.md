# 进程间通信

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\1.jpg)

## 通信管道

```
注意：1.muliprocessing中管道通信之能用于有亲缘关系的进程中，就是父子进程或兄弟之间的
    2.管道对象只能在父进程中创建，子进程通过父进程获取
```

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\2.jpg)

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\3.jpg)

```python
"""
管道通信
注意：1.muliprocessing中管道通信之能用于有亲缘关系的进程中，就是父子进程或兄弟之间的
    2.管道对象只能在父进程中创建，子进程通过父进程获取

"""
from multiprocessing import  Process,Pipe
# 创建管道

fd1,fd2 = Pipe()#False 单向 单项管道 单项调用fd1 只能调用recv, fd2只能调用send
def app1():
    print("启动app1,请登陆")
    print("请求app2授权")
    fd1.send("app1 请求登陆") #写入管道
    data = fd1.recv()
    if  data:
        print('登陆成功',data)

def app2():
    data = fd2.recv() #阻塞等待读取管道内容
    print(data)
    fd2.send(('Dave','123')) #可以发送任意类型数据

p1 =Process(target=app1)
p2 =Process(target=app2)
p1.start()
p2.start()
p1.join()
p2.join()
```

消息队列



![](D:\python 学习笔记\数据结构\day10进程间通信\pic\4.jpg)

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\5.jpg)

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\6.jpg)

```python
"""
消息队列
注意：消息队列符合先进先出原则

"""
from multiprocessing import Queue,Process
from  random import randint
import  time
#创建消息队列
q =Queue(5)#最大长度4
def handle():
    for i in range(6):
        x = randint((1,34))
        q.put(x)#消息入队
    q.put(randint(1,16))

def reques():
    while True:
        print('摇啊摇')
        time.sleep(2)
        try:
            print(q.get(3),edn='') #消息出对 timeout 3秒
        except:
            break

p1 =Process(target=handle)
p2 = Process(target= reques)
p1.start()
p2.join()
p1.join()
p2.join()
```

# 共享内存只能保留1次写入的内容

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\7.jpg)

优点：速度快 效率高

缺点：只能保留1次写入内容

c必须是字节串

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\8.jpg)

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\9.jpg)



```python
"""
value 开辟单一共享内存空间
注意：共享内存中只能有1个值
"""

from multiprocessing import Process,Value
import time
import  random

#创建共享内存
money =Value('i',5000)
#操作共享内存
def man():
    for i in range(30):
        time.sleep(0.2)
        money.value +=random.randint(1,000)

def girl():
    for i in range(30)
        time.sleep(0.2)
        money.value -= random.randint((100,800))

p1 = Process(target=man)
p2 = Process(target=girl)
p1.start()
p2.start()
p2.join()
p1.join()

#获取共享内存
print('每月余额:',money.value)
```

array 列表里的元素要同一个类型 i c f

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\10.jpg)

```python
"""
array 一般是列表或字节串
"""
from multiprocessing import Process,Array
#创建共享内存
shm = Array('i',[1,2,3,4,5])
#shm = Array('i',5) #表示初始开辟5个整形空间 [0,0,0,0,0]
#shm =Array('c',b'hello')#必须是字节串
#print(shm.value) 打印字节串

def fun():
    #创建的共享内存对象可迭代
    for i in shm:
        print(i)
    shm[1] = 1000 #修改共享内存

p = Process(target=fun)
p.start()
p.join()
```



## 信号量（信号灯塔）

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\11.jpg)

![](D:\python 学习笔记\数据结构\day10进程间通信\pic\12.jpg)

```
"""
信号量
思路：信号量数量相当于资源，执行任务必须小号资源
"""

from multiprocessing import Process,Semaphore

from  time import  sleep
import  os

#创建信号量(最多允许3个任务同时执行）
sem = Semaphore(3)

#任务函数
def handle():
    sem.acquire()#想执行任务必须小号1个信号量
    print('%s执行任务'%os.getpid())
    sleep(2)
    print('%s执行任务完毕'%os.getpid())
    sem.release() #任务执行完了归还信号量。

#执行10个任务
for i in range(10):
    p = Process(target=handle)
    p.start()
```