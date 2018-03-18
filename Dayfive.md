#### 画流程图便于理解过程

#### 服务器重定向 使用Scrapy 

## 使用API -- Application Programming Interface 应用编程接口
#它们为不同的应用提供了方便友好的接口。不同的开发者用不同的架构，甚至不同的语言编写软件都没问题——因为 API 设计的目的就是要成为一种通用语言，让不同的软件进行信息共享
利用HTTP从网络服务获取信息有四种方式：
**GET
POST
PUT
DELETE**
GET 请求给予服务信息
POST "请把信息保存到你的数据库里"
PUT  请求来更新一个对象的信息
DELETE 删除一个对象

两种返回信息格式 XML 和 JSON

案例一 Echonest

案例二 Twitter API   请求限制： 每十五分钟十五次和每十分钟180次，1分钟获得12次Twitter基本信息，但一分钟只能获得一次Follower信息
python twitter 库
```
from twitter import Twitter
t = Twitter(auth=OAuth(<Access Token>,<Access Token Secret>, <Consumer Key>,<Consumer Secret>))
pythonTweets = t.search.tweets(q = '#python')
print(pythonTweets)
```
推文以JSON格式数据（JSON字段和内容都用双引号，这是 Python 字符串打印形式的内容）保存
完整文档在https://github.com/sixohsix/twitter 上查看

案例三 Google API

#### 解析JSON 数据

Python 使用了一种更加灵活的方式，把 JSON 转换成字典，JSON 数组转换成列表，JSON 字符串转换成 Python 字符串
import json
jsonString ='{"arrayOfNums":[{"number":0},{"number":1},{"number":2}], "arrayOfFruits":[{"fruit":"apple"},{"fruit":"banana"}, {"fruit":"pear"}]}'
jsonObj = json.loads(jsonString)
