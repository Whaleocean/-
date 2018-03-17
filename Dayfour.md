html_doc可以转化为BeautifulSoup对象，按照 **标准的缩进格式的结构输出**
简单浏览结构化数据的方法
```
soup.tag        #显示一整个标签的内容
soup.tag.name   #显示标签名
soup.tag.string #显示标签内容
soup.tag["attr"]#显示标签中属性内容

从文档中找到所有<a>标签
soup. find_all("a")

从文档中找到所有在<a>中的连接
for link in soup.find_all("a"):
  print(link.get("href")
  
从文档中获得文字内容
soup.get_text() #去掉了超链接，图片等超文本的内容
```

**文档会被转换为Unicode,并且HTML的实例都会被转换成Unicode编码**
BeautifulSoup 将HTML文档转化为一个复杂的树形结构，每个节点都是python对象：Tag,NavigableString,BeautifulSoup,Comment.

```
soup = BeautifulSoup('<b class="boldest">Extremely bold</b>')
tag = soup.b
type(tag)
# <class 'bs4.element.Tag'>
```
Tag 两种重要的features *name,attribute*

Tag都有自己的名字，通过.name获取
Tag有任意数量的attributes.  
**The tag \<b id="boldest"> has an attribute “id” whose value is “boldest”**
可以通过类似字典的方式获得attributes
soup.b['id']
#u'boldest'
也可以通过.attrs 获得这个attribute-value的字典
tag.attrs
#{u'id': 'boldest'}

```
#A string corresponds to a bit of text within a tag. 
#Beautiful Soup uses the NavigableString class to contain these bits of text
type(tag.string)
-><class 'bs4.element.NavigableString'>
```
## 不可以对固定位置的string进行修改，但是可以replace one string with another using replace_with()
```
tag.string.replace_with('A new NaviableString')
```
如果我们想在外界正常地使用NavigableString,需要把他转化成Unicode地string，否则将占用大量内存


