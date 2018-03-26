Session 对象持续跟踪会话信息 - cookie，header，HTTP协议运行信息-HTTPAdapter

#### HTTP基本接入认证
Requests.auth模块专门处理HTTP认证. 
```
import requests 
from requests.auth import AuthBase 
from requests.auth import HTTPBasicAuth
auth = HTTPBasicAuth('ryan', 'password')
r = requests.post(url="http://pythonscraping.com/pages/auth/login.php", auth= auth)
print(r.text)
```
一个 HTTPBasicAuth 对象作为 auth 参数传 递到请求中

#### 表单问题
表单是网络恶意机器人（malicious bots）酷爱的网站切入点。你当然不希望机器人创建垃 圾账号，占用昂贵的服务器资源，或者在博客上提交垃圾评论。因此，新式的网站经常在 HTML中使用很多安全措施，让表单不能被快速穿越

有验证码 CAPTCHA - 利用Python图像处理和文本识别的方法
莫名错误 - 蜜罐 honey pot， 隐含字段 hidden field 以及其他保护网页表单的安全措施

#### Javascript
##### 在Python中用Selenium执行JavaScript


### 图像识别和文字处理

####  Pillow
http://pillow.readthedocs.org/
#### Tesseract
OCR库 
Tesseract是Python命令行工具，并不能用import语句导入库
#### Numpy
线性代数以及科学计算方法
