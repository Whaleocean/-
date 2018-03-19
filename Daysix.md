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
CSV（Comma-Separated Values，逗号分隔值）是存储表格数据的常用文件格式
> The csv module’s reader and writer objects read and write sequences. Programmers can also read and write data in dictionary form using the DictReader and DictWriter classes.

###### MySQL
###### 基本命令

\> CREATE DATABASE <name>; 创建数据库
\> CREATE TABLE pages (id BIGINT(7) NOT NULL AUTO_INCREMENT, title VARCHAR(200), content VARCHAR(10000), created TIMESTAMP DEFAULT CURRENT_TIMESTAMP, PRIMARY KEY (id));
创建数据表需要至少一列，把字段的定义放进一个带括 号的、内部由逗号分隔的列表中，在字段定义列表的最后，还要定义一个“主键”（key）
每个字段的定义由三个部分组成-  1.名称
                            2.数据类型
                            3.其他可选属性 (NOT NULL AUTO_INCREMENT)
*插入数据*
  > INSERT INTO pages (title, content) VALUES ("Test page title", "This is some te st page content. It can be up to 10,000 characters long."); 
选择数据
  >SELECT * FROM pages WHERE id = 2;
会返回 title 字段里包含“test”的所有行（% 符合表示 MySQL 字符 串通配符）的所有字段
  >SELECT * FROM pages WHERE title LIKE "%test%"
  
  >DELETE FROM pages WHERE id = 1;
##### 使用 PyMySQL  
import pymysql
conn = pymysql.connect(host='127.0.0.1', unix_socket='/tmp/mysql.sock', user='root', passwd=None, db='mysql')

import pymysql

#打开数据库 （如果连接失败会报错）
#db = pymysql.connect(host = '127.0.0.1', port = 3306, user = 'minbo', passwd = '123456', db = 'pythontest')
db = pymysql.connect(host = '127.0.0.1', port = 3306, user = 'minbo', passwd = '123456', db = 'pythontest', charset="utf8")

#获取游标对象
cursor = db.cursor()

#执行sql查询操作
sql_select = "select version()"
cursor.execute(sql_select)

#使用fetchone()获取单条数据
data = cursor.fetchone()
print("DB version is : %s" % data)

#如果user表存在，就删除
cursor.execute("drop table if exists user")

#创建表user
sql_create = "create table user(id int, name varchar(10)) engine = innodb charset = utf8"
cursor.execute(sql_create)

#插入操作
sql_insert = '''insert into user(id, name) values (2, "李明")'''
try:
    #执行sql
    cursor.execute(sql_insert)
    db.commit()
except:
    #发生异常
    db.rollback()

#查询操作
sql_select = '''select * from user'''
try:
    #执行sql语句
    cursor.execute(sql_select)
    #获取所有记录列表
    result = cursor.fetchall()
    for row in result:
        id = row[0]
        name = row[1]
        print("id = %d, name = %s" % (id, name))
except:
    print("Error: unable to fecth data")

#执行事务
'''事务机制可以确保数据的一致性
    1.事务有四个属性：原子，一致，隔离，持久；通常称为ACID
    2.Python DB API2.0的事务提供了两个方法：commit 和 rollback
    3.对于支持事务的数据库，在python数据库编程中，当游标建立之时，就自动开始了一个隐形的数据库事务，
    这个区别于mysql客户端，commit()方法提交所有的事务，rollback()方法回滚当前游标的所有操作。每个方法都开启了一个新的事务'''
#例子
sql_insert = '''insert into test(id, name) values (1, 'china')'''
try:
    cursor.execute(sql_insert)
    db.commit()
except:
    db.rollback()

print("end")
#关闭连接
db.close()
