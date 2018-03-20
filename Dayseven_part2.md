import pymysql.cursors

#Connect to the database
connection = pymysql.connect(host='localhost',
                             user='user',
                             password='passwd',
                             db='db',
                             charset='utf8mb4',
                             cursorclass=pymysql.cursors.DictCursor)

connection = pymysql.connect(host='127.0.0.1',user='root',password='Gjy990325',db='test',charset='utf8',port = 3306,cursorclass=pymysql.cursors.DictCursor)

Localhost - 127.0.0.1
db - 以及存在的database
port - 3306

#### 使用python收发邮件
Python 有两个包可以发送邮件：smtplib 和 email
*使用的 MIMEText 对象*，为底层的 MIME（Multipurpose Internet Mail Extensions，多用途互联网邮件扩展类型）协议传输创建了一封空邮件，最后通过高层的 SMTP 协议发送出去。**MIMEText 对象 msg 包括收发邮箱地址、邮件正文和主题**，Python 通 过它就可以创建一封格式正确的邮件
**smtplib 模块用来设置服务器连接的相关信息**。就像 MySQL 服务器的连接一样，这个连接 必须在用完之后及时关闭，以避免同时创建太多连接而浪费资源
import smtplib
from email.mine.text import MIMEText
msg = MIMEText("The body of the mail is here")
msg['Subject'] = "A Email Alert"
msg['From'] = "3170113800@zju.edu.cn"
msg['To'] = "2364167200@qq.com"
s = smtp.SMTP("127.0.0.1")
s.send_message(msg)
s.quit
