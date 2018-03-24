### 数据清洗
n-gram 模型 - 文字或语言中连续n个连续的单词组成的序列。
在进行自然语言分析时， 使用n-gram来寻找常用词组，可以很容易地把一句话分解成若干个文字片段
##### 如何获取格式合理的 n-gram

```
def ngrams(input,n):
    input = input.split(" ")
    output = []
    for i in range(len(input)-n+1):
        output.append(input[i:i+n])
    return output

#获得所有的ngram词组
```
但是会出现编码不一致的字符and 每一个单词都会和其后n-1个单词组成一个ngram， 是不便于管理的数据集
可以使用re去调整
###### re.sub-subtitute
re.sub(pattern, repl, string, count=0, flags=0)
Return the string obtained by **replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl**. If the pattern isn’t found, string is returned unchanged. repl can be a string or a function; **if it is a string, any backslash escapes in it are processed**. That is, \n is converted to a single newline character, \r is converted to a carriage return, and so forth. Unknown escapes such as \& are left alone. Backreferences, such as \6, are replaced with the substring matched by group 6 in the pattern. 
###### bytes（source[,encoding[,error]])
用bytes函数把所有字符都编码位UTF-8格式
在decode解码为decode， 避免字符串中各种格式都出现
errors -- 设置不同错误的处理方案。默认为 'strict',意为编码错误引起一个UnicodeError。 其他可能得值有 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace' 以及通过 codecs.register_error() 注册的任何值。'ignore' 编码错误就进行忽略！
##### 额外的要求
可以增加一些规则来处理数据，或者制定一些规则让数据更加规范
1.剔除单字符的'单词'，除非这个字符是'i','a'
2.剔除维基百科的引用标记([1])
3.提出标点符号
我们可以把规则都移出来，单独建一个函数，cleanIput
```
def cleanInput(input):
    input = re.sub("\n+"," ",input)
    input = re.sub(" +"," ",input)
    input = re.sub("\[[0_9]*\]","",input)
    input = bytes(input,encoding = "utf-8",errors = 'ignore')
    input = input.decode(encoding = 'ascii',errors = 'ignore')
    clean = []
    input = input.split(" ")
    for i in input:
        i = i.strip(string.punctuation)
        if len(i) > 1 or i.lower() =="a" or i.lower() == "i":
            clean.append(i)
    return clean
```
**import string 和 string.punctuation 来获取 Python 所有的标点符号**
在循环体中用 item.strip(string.punctuation) 对内容中的所有单词进行清洗，单词两端 的任何标点符号都会被去掉，但带连字符的单词（连字符在单词内部）仍然会保留。

### 数据标准化
上面进行清洗过的数据包含太多重复的2-gram序列，程序把没给个2-gram都加入了列表，没有统计过序列的频率
然而 Python的字典对象是无序的，需要使用collections库中的OrderedDict，Counter
Counter只能作用于str类型的数据，对ngram的List无效，所以要转化成str(n-gram)
当然考虑到**大小写因素，可以在cleaInput里使用 input = input.upper()，统一大小写**
### NLTK natural language Toolkit 自然语言工具包
用于识别和 标记英语文本中各个词的词性（parts of speech）
