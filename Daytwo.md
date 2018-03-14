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
  
