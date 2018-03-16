## 处理子标签
**导航树/文档树** —> html文档中的文件结构，由父子标签组成
有父标签，子标签(children)，后代标签(descendant(s))
```
#获得子标签 .children
#获得后代标签 .descendants
for child in soup.find("table",{"id":"giftList"}):
  print(child)
#b4 文档里还称之为子节点，后代节点，(父节点)
```
## 处理兄弟标签
** next_siblings**  返回标签后面的兄弟标签，值得注意的是，不会返回当前标签的内容
``` 
from urllib.request import urlopen
from bs4 import BeautifulSoup
html = urlopen("http://www.pythonscraping.com/pages/page3.html")
soup = BeautifulSoup(html)
for brother in soup.find("table",{"id":"giftList"}).next_siblings
  print(brother)
```
## 父标签的处理
```
from urllib.request import urlopen 
from bs4 import BeautifulSoup
html = urlopen("http://www.pythonscraping.com/pages/page3.html") 
bsObj = BeautifulSoup(html) 
print(bsObj.find("img",{"src":"../img/gifts/img1.jpg" }).parent.previous_sibling.get_text())
```
这段代码会打印 ../img/gifts/img1.jpg 这个图片对应商品的价格（这个示例中价格是 $15.00）。
这是如何实现的呢？
下面的图形是我们正在处理的HTML页面的部分结构，用数字表示步 骤的话： 
• <tr> 
  — <td> 
  — <td> 
  — <td>(3) 
  — "$15.00" (4)
— <td>(2) 
  — <img src="../img/gifts/img1.jpg"> 
  (1)选择图片标签 src="../img/gifts/img1.jpg"； 
  (2) 选择图片标签的父标签（在示例中是 <td> 标签）； 
  (3) 选择 <td> 标签的前一个兄弟标签 previous_sibling（在示例中是包含美元价格的 <td> 标签）；
  (4) 选择标签中的文字，“$15.00”
  
# 用正则表达式处理标签
  re.compile -> Compile a regular expression pattern into a regular expression object
  用于 findALL() & find()
```
  #sample -> img src="../img/gifts/img4.jpg"
  #for img in soup.findAll("img",{"src":re.compile(r"../img/gifts/img\d.jpg"}
from urllib.request import urlopen 
from bs4 import BeautifulSoup 
import re
html = urlopen("http://www.pythonscraping.com/pages/page3.html") 
bsObj = BeautifulSoup(html)
images = bsObj.findAll("img",{"src":re.compile("\.\.\/img\/gifts/img.*\.jpg")}) 
for image in images: 
  print(image["src"])
  print(image)
   #image 打印出<img src="../img/gifts/img3.jpg"/> 标签内容
   #image["src"] 打印出 ../img/gifts/img3.jpg 内容
```
## 获得标签属性
get_text()可以获得内容去掉标签，但有些内容是放在标签里面的比如标签的属性

在网络数据采集时你经常不需要查找标签的内容，而是需要查找标签属性。
 比如**标签\<a\> 指向 的 URL 链接包含在 href 属性中**，或者 **\<img\> 标签的图片文件包含在 src 属性中**，这时获取标签属性就变得非常有用了
  myTag.attrs              #返回的是一个字典对象（类字典，<   >） 
  myTag.attrs["property"]  #可以通过索引获得和操作这些属性
  #<xxx  x ="xxxx" > 是一个字典对象，可以通过 .xxx["x"] 来 获取 “xxxx”属性

## lambda表达式在findAll中的作用
BeautifulSoup 允许我们把特定函数类型当作 findAll 函数的参数。唯一的限制条件是这些 **函数必须把一个标签作为参数且返回结果是布尔类型**。BeautifulSoup 用这个函数来评估它 遇到的每个标签对象，**最后把评估结果为“真”的标签保留**，把其他标签剔除

soup.findAll(lambda tag: len(tag.attrs) == 2)

超越BeaautifulSoup 的库
lxml
HTML paprser 
  
