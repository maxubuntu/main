# TCP套接字之HTTp传输

![](.\pic\1.jpg)

![](.\pic\3.jpg)

![](.\pic\2.jpg)

# http请求(request)

请求行和空行必须要有，请求体头和请求体不一定要有  

![](.\pic\4.jpg)

![](.\pic\5.jpg)

请求头：都是键值对组成的 

![](.\pic\6.jpg)

![](.\pic\7.jpg)



#http相应(resoponse)

相应行和空行是必须的

![](.\pic\8.jpg)

![](.\pic\9.jpg)

![](.\pic\10.jpg)

```python
"""
htttp 请求
"""

from socket import *
s =socket()
s.setsockopt(SOL_SOCKET,SO_REUSEADDR,1)
s.bind(('0.0.0.0',9000))
s.listen(3)
c,addr = s.accept()
print('connect from',addr)
data =c.recv(4096)
print(data.decode())

# response = "HTTP/1.1 200 ok\n"
# response = repsonse+'Content-Type/html\n\n'
# response = repsonse +"<h1>hello world</h1>"
response ="""
HTTP/1.1 200
Content-Type/html

<h1>hello world</h1>
"""
c.send(response.encode())
c.close()
s.close()
```



 ```python
"""
基本要求：
1.获取来自浏览器的请求，
2.判断如果请求内容是/ 经index.hem返回给客户端
3.如果请求的是其他内容，则返回404
"""
from socket import *
s = socket()
s.setsockopt(SOL_SOCKET,SO_REUSEADDR,1)
text3 = """HTTP/1.1 200 ok
Content-Type: text/html

"""
text4 = """HTTP/1.1 404 Not Found
Content-Type: text/html

  """
s.bind((('0.0.0.0',9004)))
def request(c):
    data = c.recv(4096)
    print(data.decode())
    data1 = data.decode().split('\n')[0]
    data2 = data1.split(' ')
    if data2[1] == '/':
        file = open('index.html', 'r')
        text1 = text3 + file.read()
        file.close()
    else:
        file = open('fail.html', 'r')
        text1 = text4 + file.read()
        file.close()
    # print(text1)
    c.send(text1.encode())

s.listen(5)
while True:
    c,addr = s.accept()
    request(c)
 ```



