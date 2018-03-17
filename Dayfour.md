html_doc可以转化为BeautifulSoup对象，按照 **标准的缩进格式的结构输出**
简单浏览结构化数据的方法
```
soup.tag        #显示一整个标签的内容
soup.tag.name   #显示标签名
soup.tag.string #显示标签内容
soup.tag["attr"]#显示标签中属性内容

从文档中找到所有<a>标签
soup. find_all("a")
```
**值得注意的是，返回的是一个*列表*，不能得到标签的attributes.**

从文档中找到所有在<a>中的连接
for link in soup.find_all("a"):
  print(link.get("href")
  
从文档中获得文字内容
```
soup.get_text()
```
**#去掉了超链接，图片等超文本的内容**

### **文档会被转换为Unicode,并且HTML的实例都会被转换成Unicode编码**
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
**也可以通过.attrs 获得这个attribute-value的字典**
tag.attrs
#{u'id': 'boldest'}

```
#A string corresponds to a bit of text within a tag. 
#Beautiful Soup uses the NavigableString class to contain these bits of text
type(tag.string)
-><class 'bs4.element.NavigableString'>
```
**不可以对固定位置的string进行修改，但是可以replace one string with another using replace_with()**
```
tag.string.replace_with('A new NaviableString')
```
如果我们想在外界正常地使用NavigableString,需要把他转化成Unicode地string，否则将占用大量内存
u_str = unicode(tag.string)

# Navigating the tree

## Navigating using tag names
soup.head
soup.body.p
*Using a tag name as an attribute will give you only the first tag by the nature
If you need to get all the <a> tags, or anything more complicated than the first tag with a certain name, you’ll need to use one of the methods described in Searching the tree, such as find_all(),which return a list*

## Navigating through child and descendant
### .centents & .children
A tag\`s children are available in **a list** called **.contents**

The BeautifulSoup object itself has children. In this case the \<html>tag is th child of the BeautifulSoup object
**A string does not have .contents**, because it cann`t contain anything #raise AttributeError

.children -> instead of getting them as a list, we can iterate over a tag\`s children using the **.children generator**

for child in title_tag.children:
 print(child)
### .descendants
contents and children only consider a tag\`s **directly children**
the .descendant let you to **iterate over all of a tag\`s children, recursively**
also a <class 'generator'>

If a tag has only one child, and that child is a NavigableString, the child is made available as .string:
```
title_tag.string
#u'The Dormouse's story'
```
If a tag’s only child is another tag, and that tag has a .string, then the parent tag is considered to have the same .string as its child:
```
head_tag.contents
#[<title>The Dormouse's story</title>]

head_tag.string
#u'The Dormouse's story'
```

If there\`s more than one thing inside a tag, you can still look at hyst the strings
Use the .strings generator rather than .string which will **return None**
.strings genaratefor string in soup.strings:
    print(repr(string))
```
for string in soup.strings:
    print(repr(string))
# u"The Dormouse's story"
# u'\n\n'
# u"The Dormouse's story"
# u'\n\n'
# u'Once upon a time there were three little sisters; and their names were\n'
# u'Elsie'
# u',\n'
# u'Lacie'
# u' and\n'
# u'Tillie'
# u';\nand they lived at the bottom of a well.'
# u'\n\n'
# u'...'
# u'\n's a generator
``` 
However, there are always alot of extra whitespace, which can be removed by using the .stripped_strings genarator instead
``` 
for string in soup.html.stripped_strings
 print(string)
``` 
##Going UP
### .parent
access a tag\`s parent with the .parent attribute
```
title.string.parent
-> <title>The Dormouse's story</title>
```
The parent of a top-level tag like <html> is the BeautifulSoup object itself:

html_tag = soup.html
type(html_tag.parent)
#<class 'bs4.BeautifulSoup'>
And the .parent of a BeautifulSoup object is defined as None:

print(soup.parent)
#None

### iterate over all of an element\`s parents with .parents (generator)
```
link = soup.a
link
# <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
for parent in link.parents:
    if parent is None:
        print(parent)
    else:
        print(parent.name)
```
这个parents..迭代出来的是整一个parents 的标签，包含tags 和NavigatingString

##Gosideways.
.next_sibling and .previous_siblings
.next_siblings and .previous_siblings

# Searching the tree




