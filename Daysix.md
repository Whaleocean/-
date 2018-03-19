###### Python 集合类型
集合无序，不会存储重复的值，如果要.add("一个已有的值") 会自动忽略，集合实际上是一个值为None的字典，采用hash算法,查询速度为0(1)

##### 存储数据
存储媒体文件有两种主要的方式：只获取文件 URL 链接，或者直接把源文件下载下来
```
可以通过媒体文件所在的URL 链接直接引用它
1.爬虫运行得更快，耗费的流量更少，因为只要链接，不需要下载文件。 
2.可以节省很多存储空间，因为只需要存储 URL 链接就可以。 
3.存储 URL 的代码更容易写，也不需要实现文件下载代码。 
4.不下载文件能够降低目标主机服务器的负载。
缺点
1.这些内嵌在你的网站或应用中的外站 URL 链接被称为盗链（hotlinking），使用盗链可 能会让你麻烦不断，每个网站都会实施防盗链措施。
2.因为你的链接文件在别人的服务器上，所以你的应用就要跟着别人的节奏运行了。
3.盗链是很容易改变的。如果你把盗链图片放在博客上，要是被对方服务器发现，很可能 被恶搞。如果你把 URL 链接存起来准备以后再用，可能用的时候链接已经失效了，或 者是变成了完全无关的内容。
4.现实中的网络浏览器不仅可以请求HTML页面并切换页面，它们也会下载访问页面上 所有的资源。下载文件会让你的爬虫看起来更像是人在浏览网站，这样做反而有好处。
```
####### urllib.request.urlretrieve 可以根据文件的 URL 下载文件
from urllib.request import urlretrieve 
from urllib.request import urlopen 
from bs4 import BeautifulSoup
html = urlopen("http://www.pythonscraping.com") 
bsObj = BeautifulSoup(html)
imageLocation = bsObj.find("a", {"id": "logo"}).find("img")["src"])
urlretrieve (imageLocation, "logo.jpg")

###### 把数据存储到CSV
