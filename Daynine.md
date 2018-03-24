urllib可以基本完成get请求得到的信息
实现POST请求，即将信息发送给服务器进行存储和分析，可以使用REQUESTS库实现
擅长处理那些复杂的 HTTP 请求、cookie、header（响应头和请求头）等内容
**表单真是的行为其实发生在processing.php，POST请求应该发生在这个页面上

### 使用Requests提交表单
只需要四行代码能够实现
```
import requests

params = {"firstname": "Ryan", "lastname": "Mitchell"}
r = requests.post(url+"/processing.php",data = params)
#r是提交表单后返回的数据
print(r.text)
```
### 单选按钮，复选框和其他输入
表单的字段可以是非常的复杂，但仍然只有两件事是需要关注的：字段名称和值
字段的名称可以查看源代码寻找**name**属性得到
当不确定一个输入字段值的数据格式，有一些工具可以追踪浏览器正在通过网站发送后者接受的GET,POST请求的内容(Cchrome 内置)

跟踪GET请求效果最好也最直接的手段是看网站的URL连接
> http://domainname.com?thing1=foo&thing2=bar
则
```
这个请求的就是下面的这种表单
<form method="GET" action="someProcessor.php">   #表单中action属性，就是表单提交后网站会显示的页面
<input type="someCrazyInputType" name="thing1" value="foo" /> 
<input type="anotherCrazyInputType" name="thing2" value="bar" /> 
<input type="submit" value="Submit" /> </form>
```
对应putjon的参数为{"thing1","foo", "thing2": "bar"}

### 提交文件和图像
<form action="processing2.php" method="post" enctype="multipart/form-data">
  Submit a jpg, png, or gif: <input type="file" name="image"><br> 
  <input type="submit" value="Upload File"> 
</form>
#网页源代码
```
import requests
files = {"uploadFile": open("....../test.jpg","rb")}
r = reuqest.post("url"+"processing2.php",file)
```
### 处理登陆和cookie
大多数网站都是用cookie来跟踪用户是否已登陆的状态信息，一旦网站验证你的登陆权证，它会将一些信息保存在浏览器cookie中
里面通常包含一个服务器生成的令牌，登陆有效时限和状态跟踪信息。网站会把这个cookie当作信息验证的证据，在你浏览给个页面时出示给服务器

为网络爬虫带来了大问题。你可以一整天只提交一次登录表单，但是如果你没有一直关注表单后来回传给你的那个 cookie，那么 一段时间以后再次访问新页面时，你的登录状态就会丢失，需要重新登录

如果在登录网站之前你想进入欢迎页面或者简介页面，会看到一个错误信息和访问前请先 登录的指令。**在简介页面中，网站会检测浏览器的 cookie，看它有没有页面已登录的设置信息**
```
import requests
params = {"username": "Ryan", "password": "password"}
r = requests.post("http://pythonscraping.com/pages/cookies/welcome.php",data = params)
print("Cookie is set to:")
print(r.cookies.get_dict())
print("---------------")
print("go to profile page...")
r = requests.get("http://pythonscraping.com/pages/cookies/profile.php",cookies = r.cookies)
print(r.text)
```
这里项欢迎页面发送一个登陆参数，然后我们从请求结果中获得了cookie，打印登陆状态的验证结果，然后通过cookie参数法cookie发送到简介页面
r.cookies ->>> cookies 参数

复杂的网站经常暗自调整cookie，或者从一开始就完全不想用cookie，那可以用Requests库的session函数解决
**会话对象(session)(通过调用requests.session()获取) 可以持续跟踪会话对象信息 -cookie，header甚至包括运行HTTP协议的信息
**

