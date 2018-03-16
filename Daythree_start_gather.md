
* 网络爬虫的本质就是一种递归方式。为了找到 URL 链接，它们必须首先获取网页内容，检查这个页面的内容，再寻找另一个URL，然后获取 URL对应的网页内容，不断循环这一过程。
* 考虑需要消耗多少网络流量，还要尽力思考能不能让采集目标的服务器负载更低一些。
```
<a class="noprint stopMobileRedirectToggle" href="//en.m.wikipedia.org/w/index.php?title=Eric_Idle&amp;mobileaction=toggle_view_mobile">Mobile view</a>
#首先这个是一个对象，可以被.findAll("a") 获得 link = soup.findAll("a")
#可以通过 link.attrs 获得一个字典对象，key是当前标签里所有class名，值为相应的属性
{'href': '//en.m.wikipedia.org/w/index.php?title=Eric_Idle&mobileaction=toggle_view_mobile', 'class': ['noprint', 'stopMobileRedirectToggle']}
分别是属性名和对应属性值，要获得属性值，可以通过 link.attrs["class_name"]
判断是否有这个属性(key) 可以用 if aimed_class in link.attrs()
```
