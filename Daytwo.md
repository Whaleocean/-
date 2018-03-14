# 异常处理

1.网页在服务器上不存在（或者获取页面时出现错误)
2.服务器错误 (url打不开，url写错了)
```
try: html = urlopen("http://www.pythonscraping.com/pages/page1.html")
except HTTPError as e: print(e) # 返回空值，中断程序，或者执行另一个方案
else: # 程序继续。注意：如果你已经在上面异常捕捉那一段代码里返回或中断（break）， # 那么就不需要使用else语句了，这段代码也不会执行
```
第一种错误会抛出HTTPError,对错误进行处理
如果服务器不存在（就是说链接 http://www.pythonscraping.com/ 打不开，或者是 URL 链接 写错了），urlopen 会返回一个 None 对象-可以增加一个判断语句检测返回的 html 是不是 None
``` 
if html is None:
  print("URL not found")
else:
  pass
# is == 区别 右转 "https://foofish.net/what-is-difference-between-is-and-euqals.html"
```
如果标签不存在
BeautifulSoup返回None对象 如果在对这个None对象操作可能会抛出错误
try:
  badContent = bsObj.nonExistingTag.anotherTag
except AttributeRError as e:
  print("Tag was not found")
else: #当没有错误发生的时候
  if badContent == None:
    print("Tag was not found")
  else:
    print(badcontent)
    
  #双重检查.
  ```
```#综合起来
from urllib import request
from bs4 import BeatifulSoup
from urllib.error import HTTPError
def get_title(url):
  try:
     html = request.urlopen(url)
  except HTTPError:
     return None
  else:
        try:
          bsObj = BeautifulSoup(html.read())
          title = bsObj.body.h1
        except AttributeError:
          return None
        else:
          return title
          
titile = get_title("http://www.pythonscraping.com/pages/page1.html")
if titile == None:
  pirnt("titile do not exist")
else:
  print(title)
```
## .findAll("Tagname",attr = {"class":"parameter"})
bdObj.Tagname 只能找到第一个标签时Tagname的Data.
调用.findAll(Tagname) 可以找到所有的带标签名的数据
参数 attr = {"class":"paramater"} 用字典形式保存的键值对去索引带有该attr的标签数据

> *这个对象是个可迭代的对象iterable，可以用for语句遍历 *
> 可以* 使用.get_text()把标签中的内容分开显示 * ### 把内容去掉标签后显示
> .get_text() 会把你正在处理的 HTML 文档中**所有的标签**都清除，然后返回 一个只包含文字的字符串。假如你正在处理一个包含许多超链接、段落和标 签的大段源 > 代码，那么 .get_text() 会把这些超链接、段落和标签都清除掉， 只剩下一串不带标签的文字。

> **BeautifulSoup 对象查找你想要的信息，比直接在 HTML 文本里查找信 息要简单得多。**
> 通常在你准备打印、存储和操作数据时，应该最后才使 用 .get_text()。一般情况下，你应该尽可能地保留HTML文档的标签结构
```
from urllib.request import urlopen
from bs4 import BeautifulSoup
html = urlopen("http://www.pythonscraping.com/pages/warandpeace.html")
bsObj = BeautifulSoup(html.read())
aimed_txt = bsObj.findAll("span",{"class":"red"})
for name in aimed_txt:
  print(name.get_txt())
```
