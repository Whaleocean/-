urllib.request 提供urlretrieve() 函数 （retrieve检索，取回)
#### urlretrieve(url, filename=None, reporthook=None, data=None)
url -> 指定读取地址的URL
filename  —> 指定保存的本地路径，如果参数未指定，会生成一个临时文件保存数据
reporthool -> 回调函数 当连接到服务器，以及相应的数据块传输完毕时会触发该回调，我们可以利用这个回调函数显示当前下载的进度
data -> 参数data 值post到服务器的数据，该方法返回一个包含filename，headers两个元素的元组，header 表示服务器的响应头

MySQL 教程
有时候数据的大小远远超过了内存（比如蓝光电影，40GB的数据），根本无法全部读入内存
为了方便程序保存和读取数据，并且通过各种条件快速查询到指定的数据，实现了Database.

表（Table）的一对多的关系是关系数据库的基础

CREATE 
source dir.sql 导入数据库文件

#### SELECT 语句从表或者视图中获取数据
表由行和列组成，如电子表格

SELECT 之后是逗号分隔列 colume_1,colume_2,colume_3 或者星号* - 表示返回所有列
FROM 表示要查询数据的表或者视图
JOIN 根据某些连接条件从其他表中获得数据
WHERE 过滤结果集中的行
GROUP BY 将一组行合成小分组，并对每个小分组应用聚合函数
HAVING 过滤器基于GROUP BY 子句定义的小分组
ORDER BY 指定用于排序的列的列表
LIMIT 限制返回行的数量

语句中 SELECT 和 FROM 是必须的
