urllib.request 提供urlretrieve() 函数 （retrieve检索，取回)
#### urlretrieve(url, filename=None, reporthook=None, data=None)
url -> 指定读取地址的URL
filename  —> 指定保存的本地路径，如果参数未指定，会生成一个临时文件保存数据
reporthool -> 回调函数 当连接到服务器，以及相应的数据块传输完毕时会触发该回调，我们可以利用这个回调函数显示当前下载的进度
data -> 参数data 值post到服务器的数据，该方法返回一个包含filename，headers两个元素的元组，header 表示服务器的响应头
