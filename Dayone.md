# 网络连接
**电脑** -发出请求头：本地路由器MAC地址和目标的IP地址
     消息体：包含对目标服务器的应用请求
**本地路由器** 接收到所有0，1比特值，把他们装成数据包packet从bob的本地MAC地址寄到目标IP地址，路由器把数据包‘盖上’自己的ip地址作为发件地址，然后通过互联网发送出去
 目标在其IP地址上收到数据包

```
from urllib.request import urlopen
html = urlopen("http://pythonscraping.com/pages/page1.html") 
print(html.read())
```
