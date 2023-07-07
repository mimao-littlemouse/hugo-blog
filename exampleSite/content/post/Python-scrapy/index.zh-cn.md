---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识 Python Scrapy
# 帖子的日期
date: 2023-07-07
# 帖子的描述
description: 初识Python Scrapy并快速对其进行了解
# 帖子的标签
tags:
  - python-scrapy
# 帖子分类
categories:
  - Python
---

# scrapy介绍
## 简要介绍

1.Scrapy是一个应用程序框架，用于对网站进行爬行和提取结构化数据，
这些结构化数据可用于各种有用的应用程序，
如数据挖掘、信息处理或历史存档
（虽然这使您能够进行非常快速的爬网（以容错的方式同时发送多个并发请求），
但Scrapy还可以通过一些设置控制爬网的礼貌性。您可以在每个请求之间设置下载延迟，
限制每个域或每个IP的并发请求量，甚至可以使用自动节流扩展来自动计算这些请求。）

2.使用Scrapy从网站中提取和存储项目，但这只是表面。Scrapy提供了许多强大的功能，使Scrapy变得轻松高效，例如：
内置支持使用扩展的CSS选择器和XPath表达式从HTML/XML源中选择和提取数据，以及使用正则表达式提取的助手方法。
一个交互式shell控制台（IPython感知），用于尝试CSS和XPath表达式来抓取数据，在编写或调试蜘蛛时非常有用。
内置支持以多种格式（JSON、CSV、XML）生成或导出并将其存储在多个后端（FTP、S3、本地文件系统）中
强大的编码支持和自动检测，用于处理外来、非标准和损坏的编码声明。
强大的可扩展性支持，允许您使用信号和定义良好的API（中间件、扩展和管道）插入自己的功能。

3.用于处理的各种内置扩展和中间件：
cookie和会话处理
HTTP功能，如压缩、身份验证、缓存
用户代理欺骗
robots.txt
爬行深度限制
Telnet控制台，用于连接到运行在Scrapy进程中的Python控制台，以反省和调试爬行器
可重复使用的蜘蛛从Sitemap和XML/CSV提要中抓取站点，自动下载与抓取的项目相关的图像（或任何其他媒体）的媒体管道，
缓存DNS解析器等等！

## scrapy基础知识
### 上篇

1.创建scrapy项目
scrapy startproject myproject [project_dir]
注意：
这将在project_dir目录下创建一个Scrapy项目
如果未指定project_dir，project_dir将与myproject相同

2.创建新的spider
格式：
scrapy genspider [-t template] <name> <domain or URL>
例如：
scrapy genspider mydomain mydomain.com
注意：
(1).如果从项目内部调用，则在当前文件夹或当前项目的spider文件夹中创建新的spider
＜name＞参数设置为spider的名称，而＜domain或URL＞用于生成allowed_domains和start_urls spider的属性
(2). -t template的用法：如下 (在 终端中输入)
>>scrapy genspider -l
Available templates:
  basic
  crawl
  csvfeed
  xmlfeed

>>scrapy genspider example example.com
Created spider 'example' using template 'basic'

>>scrapy genspider -t crawl scrapyorg scrapy.org
Created spider 'scrapyorg' using template 'crawl'
注意：这只是一个基于预定义模板创建spider的快捷命令，
但肯定不是创建spider的唯一方法。您可以自己创建spider源代码 .py文件，而不用使用此命令

3.一些scrapy命令
(1).获取命令的帮助信息
scrapy genspider [-t template] <name> <domain or URL>
scrapy <command> -h

(2).查看所有可用命令
scrapy -h

4.全局命令
(1).startproject	scrapy startproject <project_name> [project_dir] 
创建scrapy项目
(2).genspider		 scrapy genspider [-t template] <name> <domain or URL> 
创建新的spider
使用预定义模板生成新蜘蛛
(3).settings 15773110606
获取设置值
(4).runspider
运行自包含的spider（不创建项目）
(5).shell
交互式scrapy控制台
(6).fetch
使用剪贴下载器获取URL
(7).view
在浏览器中打开URL，如Scrapy所示
(8).version
打印scrapy版本
5.项目命令
(1).crawl	运行spider程序
(2).check	检查蜘蛛合同
(3).list	列出可用spider
(4).edit	编辑spider
(5).parse	解析URL（使用其spider）并打印结果
(6).bench 	运行快速基准测试
(7).fetch 	使用spider下载器获取URL
运行快速基准测试
5.1命令介绍
爬取spider (命令：crawl )
开始用crawl进行爬取
scrapy crawl <spider>
支持的选项：
-h、 --help：显示帮助消息并退出
-a NAME=VALUE：设置spider参数（可以重复使用该选项，例如: -a tag='humer' -a url='demain.com' ....等等）
--output FILE或-o FILE：将scrapy的项目附加到FILE的末尾（使用-表示stdout），以定义格式，在输出URI的末尾设置冒号（即-o FILE:format）
--overwrite-output FILE或-O FILE：将scrapy项目转储到FILE中，覆盖任何现有文件，以定义格式，在输出URI的结尾设置冒号（即-O FILE:format）
--output-format FORMAT或-t FORMAT：定义用于转储项的格式的方法已被弃用，不能与-O结合使用
例如：
 >>scrapy crawl myspider
[ ... myspider starts crawling ... ]

>>scrapy -o myfile:csv myspider
[ ... myspider starts crawling and appends the result to the file myfile in csv format ... ]

>>scrapy -O myfile:json myspider
[ ... myspider starts crawling and saves the result in myfile in json format overwriting the original content... ]

>>scrapy -o myfile -t csv myspider
[ ... myspider starts crawling and appends the result to the file myfile in csv format ... ]

check命令（检查spider是否有语法错误）
scrapy check [-l] <spider>
例如：
>>scrapy check -l
first_spider
  * parse
  * parse_item
second_spider
  * parse
  * parse_item

>>scrapy check
[FAILED] first_spider:parse_item
>>> 'RetailPricex' field is missing

[FAILED] first_spider:parse
>>> Returned 92 requests, expected 0..4

list命令（列出当前项目中所有可用的spider 输出是每行一个spider）
scrapy list
例如：
>>scrapy list
spider1
spider2

edit命令
scrapy edit <spider>
使用editor环境变量中定义的编辑器或（如果未设置）editor设置编辑给定的spider。
该命令仅作为最常见情况下的快捷方式提供，开发人员可以自由选择任何工具或IDE来编写和调试spider。
例如：
 scrapy edit spider1

fetch命令
scrapy fetch <url>
使用Scrapy下载器下载给定的URL，并将内容写入标准输出
这个命令的有趣之处在于它获取页面，spider将如何下载它的页面：
例如，如果spider具有覆盖USER AGENT的USER_AGENT属性，它将使用该属性。
因此，该命令可用于“查看”spider如何获取特定页面。
如果在项目外部使用，则不会应用特定的spider行为，
它将只使用默认的Scrapy下载器设置。
支持的选项：
--spider=SPIDER：绕过spider自动检测和强制使用特定spider
--headers：打印响应的HTTP头，而不是响应的正文
--no-redirect：不遵循HTTP 3xx重定向（默认遵循它们）
例如:
>>scrapy fetch --nolog http://www.example.com/some/page.html
[ ... html content here ... ]

>>scrapy fetch --nolog --headers http://www.example.com/
```
{'Accept-Ranges': ['bytes'],
 'Age': ['1263   '],
 'Connection': ['close     '],
 'Content-Length': ['596'],
 'Content-Type': ['text/html; charset=UTF-8'],
 'Date': ['Wed, 18 Aug 2010 23:59:46 GMT'],
 'Etag': ['"573c1-254-48c9c87349680"'],
 'Last-Modified': ['Fri, 30 Jul 2010 15:30:18 GMT'],
 'Server': ['Apache/2.2.3 (CentOS)']}
```
parse命令


bench

***

### 下篇

1.一个scrapy项目，可用有多个子项目：（即：一个scrapy项目的根目录，可用有多个项目进行共享）
通过配置scrapy.conf 中的 settings配置项中，进行配置：
默认情况下：
[settings]
default = myproject.settings
设置配置：
[settings]
default = myproject1.settings	#设置默认的项目
project1 = myproject1.settings	#设置项目1的别名
project2 = myproject2.settings #设置项目2的别名
注意：
设置完之后，项目的运行，默认是按default项目进行运行，所以，可用使用下面命令更改默认设置：
(在终端中，运行下面命令)
>>scrapy settings --get BOT_NAME
Project 1 Bot
>> export SCRAPY_PROJECT=project2
>> scrapy settings --get BOT_NAME
Project 2 Bot

***

### scrapy安装和使用

1.支持的python版本：
Scrapy需要Python 3.7+，要么是CPython实现（默认），要么是PyPy实现（请参阅替代实现）

使用python进行安装，或其他方式安装
(个人喜欢使用python中的pip进行安装（并使用 virtualenv虚拟环境下进行安装）这也是强烈推荐的安装方式(在虚拟环境中安装))
（这样就可以最大程度上避免出现安装错误，并不会破环原本环境）
pip3 install scrapy

注意：值得了解的事情
Scrapy是用纯Python编写的，它依赖于几个关键的Python包（其中包括）：
lxml，一种高效的XML和HTML解析器
parsel是一个基于lxml编写的HTML/XML数据提取库，
w3lib，用于处理URL和网页编码的多用途助手
twisted，一种异步网络框架
cryptography和pyOpenSSL，以满足各种网络级安全需求
其中一些软件包本身依赖于非Python软件包，这些软件包可能需要额外的安装步骤，具体取决于您的平台
如果出现与这些依赖项相关的任何问题，请参阅各自的安装说明：
lxml模块安装
cryptography模块安装

2.在ubuntu中安装,前提是不使用python的时候，安装方式，如果 ubuntu中，已经有python virtualenv环境了，则于个人安装方式一致
Ubuntu 14.04 或 以上版本适用：
(ubuntu 14.04一下就不用考虑使用scrapy了，因为这也不可能)
要在Ubuntu（或基于Ubuntu的）系统上安装Scrapy，您需要安装这些依赖项：
sudo apt-get install python3 python3-dev python3-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev
然后，再安装virtualenv virtualenvwrapper，这安装方法，可再csdn中查到
安装相关依赖后，则激活进入 virtualenv后，安装：
pip3 install scrapy

3.创建项目
scrapy startproject 项目名称
使用命令，创建的目录如下：
项目名称/
	项目名称/		#project的Python模块，您将从这里导入代码
		__init__.py
		spiders/	#稍后放置spider的目录
			__init__.py
		items.py	#项目项定义文件
		middlewares.py	#项目中间件文件
		pipelines.py	#项目管道文件
		settings.py	#项目设置文件

	scrapy.cfg		#部署配置文件
		
第一步，创建自己的spider
介绍：spider是你定义的类，Scrapy用来从网站（或一组网站）中抓取信息
它们必须将Spider子类化，并定义要发出的初始请求，
可选地，如何跟踪页面中的链接，以及如何解析下载的页面内容以提取数据。
操作：
在项目的目录下的spiders文件夹下，创建：要做爬取的数据或功能名称_spider.py 进行命名
（例如：quotes_spider.py 我要爬取名言有关的数据，则用quotes_spider.py进行命名（推荐这样做，当然自己可以随便起名字））
quotes_spider.py中的内容：

```python
# 导入模块
from pathlib import Path
import scrapy
# 书写spider类
class QuotesSpider(scrapy.Spider):
    name = "quotes"  # name：标识蜘蛛。它在项目中必须是唯一的，也就是说，不能为不同的蜘蛛设置相同的名称

    # start_requests（）：必须返回一个可迭代的请求（您可以返回一个请求列表或编写一个生成器函数）
    # Spider将从中开始爬网 后续请求将从这些初始请求中依次生成
    def start_requests(self):  
        urls = [
            'https://quotes.toscrape.com/page/1/',
            'https://quotes.toscrape.com/page/2/',
        ]	#存放需要请求的url地址列表
        for url in urls:	#循环遍历每一个要请求的url地址
            yield scrapy.Request(url=url, callback=self.parse)  #迭代的返回每一个请求的响应至parse

    # parse（）：一个将被调用以处理为每个请求下载的响应的方法
    # response参数是TextResponse的一个实例，它保存页面内容，并有其他有用的方法来处理它
    # parse（）方法通常解析响应，将抓取的数据提取为dict，还可以找到新的URL，并从中创建新的请求（Request）
    def parse(self, response):
        page = response.url.split("/")[-2]  #根据url来获取页面名称
        filename = f'quotes-{page}.html' #获取页面名称来作为文件名
        Path(filename).write_bytes(response.body) #将获取到的内容存放至文件中
        self.log(f'Saved file {filename}')   #输出打印日志
```

4.书写完之后，运行spider:
将目录切换到项目根目录下：
打开cmd或终端输入：scrapy crawl quotes  去运行spider
运行结果结构如下：
```log
... (omitted for brevity)
日期 时间 [scrapy.core.engine] INFO: Spider opened # 这是spider运行开始的标志
日期 时间 [scrapy.extensions.logstats] INFO: Crawled 0 pages (at 0 pages/min), scraped 0 items (at 0 items/min)
日期 时间 [scrapy.extensions.telnet] DEBUG: Telnet console listening on 127.0.0.1:6023
日期 时间 [scrapy.core.engine] DEBUG: Crawled (404) <GET https://quotes.toscrape.com/robots.txt> (referer: None)
日期 时间 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/1/> (referer: None)
日期 时间 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/2/> (referer: None)
日期 时间 [quotes] DEBUG: Saved file quotes-1.html	#这是打印的日志信息
日期 时间 [quotes] DEBUG: Saved file quotes-2.html  #这是打印的日志信息
日期 时间 [scrapy.core.engine] INFO: Closing spider (finished) # 这是spider运行结束的标志
...
```

5.Scrapy调度Scrapy.Request对象，该对象由spider的start_requests方法返回。在接收到每个响应时，
它实例化response对象并调用与请求相关联的回调方法（在本例中为parse方法），将响应作为参数传递
(注意：您可以只定义一个带有URL列表的start_URLs类属性，
而不是实现一个从URL生成scrapy.Request对象的start_requests()方法
然后，start_requests()的默认实现将使用此列表为spider创建初始请求：)
即：（可以这样）
```python
# 导入模块
from pathlib import Path
import scrapy

class QuotesSpider(scrapy.Spider):
    name = "quotes"
    # 就这样定义一个 start_urls属性即可（最简单的定义方式）
    # 也会调用parse()方法来处理这些URL的每个请求，即使我们没有明确告诉Scrapy这样做
    # 这是因为parse()是Scrapy的默认回调方法，在没有明确指定回调的请求时调用该方法
    start_urls = [
        'https://quotes.toscrape.com/page/1/',
        'https://quotes.toscrape.com/page/2/',
    ]

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = f'quotes-{page}.html'
        Path(filename).write_bytes(response.body)
```

***

## 命令行模式下的巧用

### 打开命令行控制台 去练习 scrapy获取数据的方式

1.学习如何使用Scrapy提取数据的最佳方法是使用ScrapyShell尝试选择器 进行运行提取
例如：scrapy shell 'https://quotes.toscrape.com/page/1/'  
(注意：在命令行中运行ScrapyShell时，请记住始终将URL括在引号中，否则包含参数（即&符号）的URL将不起作用
在python中可以用双引号和单引号 包含字符串，但在windows中，单引号是字符，只有双引号才能包含字符串，
所以，在windows中请改用双引号)
运行结果：
```log
[ ... Scrapy log here ... ]
日期 时间 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://quotes.toscrape.com/page/1/> (referer: None)
[s] Available Scrapy objects:
[s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
[s]   crawler    <scrapy.crawler.Crawler object at 0x7fa91d888c90>
[s]   item       {}
[s]   request    <GET https://quotes.toscrape.com/page/1/>
[s]   response   <200 https://quotes.toscrape.com/page/1/>
[s]   settings   <scrapy.settings.Settings object at 0x7fa91d888c10>
[s]   spider     <DefaultSpider 'default' at 0x7fa91c8af990>
[s] Useful shortcuts:
[s]   shelp()           Shell help (print this help)
[s]   fetch(req_or_url) Fetch request (or URL) and update local objects
[s]   view(response)    View response in a browser
>>>
```
```log
使用shell，您可以尝试使用CSS和响应对象选择元素,例如：
>>>response.css('title')
结果为：
[<Selector xpath='descendant-or-self::title' data='<title>Quotes to Scrape</title>'>]
或提取其中的文本：
>>>response.css('title::text').getall()
结果为：
['Quotes to Scrape']
```

# 使用 re正则表达式进行提取数据，避免了getall() get()都提取不了的情况
2.介绍 get()  getall() （如果没有使用get getall re 这些方法，则还是一个Selector对象 也就是说还可以继续嵌套）
其实 response.get() 或 response.getall() 等，都是 response.selector.get() .getall()等的快捷书写方式
低版本中，get()是使用extract_first()  getall()是使用extract() ，而extract() extract_first() 两者都没有被弃用，都还可以使用，只是官方觉得get getall 更为简介
无论是Selector 还是SelectorList 去调用get getall 返回的结果类型一致（get还是返回第一个匹配字符串 getall 返回所有匹配的字符串列表）
(1).调用.get()的结果是一个字符串，选择器返回第一个结果，没有任何返回时，则会返回 None，也可以设置默认值,.get(default="默认值")
(2).调用.getall()的结果是一个列表，选择器可能返回多个结果，没有任何返回时，则会返回  [ ] (空列表)
(3).调用re() 正则表达式来 返回符合正则表达式的返回结果

例如
1.get()方法：
```log
>>>response.css('title::text').get()
有结果时：
'返回的结果字符串'
没有结果时：
None
>>>response.css('title::text').get(default='not-found')
有结果时：
'返回的结果字符串'
没有结果时：
'not-found'
```

2.getall()方法：
```log
>>>response.css('title::text').getall()   #不需要设置默认值，没有结果时，会默认返回空列表 [ ]
有结果时：
['','']  字符串列表
没有结果时：
[ ]

（注意：对于get()获取到的结果：可以通过 is None   is not None 来判断是否获取到数据 ）
```

3.selector的attrib属性
```log
可以使用Selector的.attrib属性查询属性，而不是xpath中使用例如'@src'的方式获取属性：
>>>[img.attrib['src'] for img in response.css('img')]
['image1_thumb.jpg','image2_thumb.jpg']
作为快捷方式，.attrib也可以直接在SelectorList上使用；它返回第一个匹配元素的属性：
>>>response.css('img').attrib['src']
'image1_thumb.jpg'
```

### 三种获取数据的方式

#### css获取数据的方式

介绍css提取数据的方法：
先准备练习提取数据方法的环境：
在项目根目录，打开终端输入：scrapy shell 网址
进入shell 控制台

1.根据W3C标准，CSS选择器不支持选择文本节点或属性值。但在web抓取环境中，选择这些非常重要，
以至于Scrapy（parcel）实现了一些非标准伪元素：
标签::text 选择标签选择器的文本节点
标签::attr(name) 选择标签选择器的属性值，其中name是要获取其值的属性的名称
标签 *::text 选择当前标签选择器上下文的所有后代文本节点
(注意：如果不知道如何使用 浏览器中的开发者工具，
可以查看https://doc.scrapy.org/en/latest/topics/developer-tools.html#topics-developer-tools中的介绍
也可以在 csdn中搜索即可得到结果，并将其学会)
```python
selector.attrib['属性'].getall()
```

#### xpath获取数据的方式

1.使用xpath来提取数据(除了css , re，Scrapy选择器还支持使用XPath表达式来提取数据)
(其实 css抓取底层也是通过转化为 xpath来实现数据提取的)
```log
>>>response.xpath('//title')
[<Selector xpath='//title' data='<title>Quotes to Scrape</title>'>]
>>>response.xpath('//title/text()').get()
'Quotes to Scrape'
其中，也可通过：
>>>from scrapy.selector import Selector 
>>>body='<html><body><span>good</span></body></html>' 
>>>Selector(text=body).xpath('//span/text').get() 
>>>"good”
进行获取
```

2.嵌套的时候，可以这样使用
```log
divs = response.xpath('//div')
div下的所有p元素：
for p in divs.xpath('.//p'): 
    print(p.get())
div p 下面的所有元素
for p in divs.xpath('p'):
    print(p.get())


下面是 xpath css 应用的一些例子：
>>>response.xpath('//base/@href').get()
'http://example.com/'
>>>response.xpath('//a[contains(@href, "image")]/@href').getall()   #contains(属性，值)  在所有该标签中查找href属性中含有image值的所有标签
```

3.注意//node[1]和（//node)[1]之间的区别:
//node[1]选择在其各自的父节点下首先出现的所有节点
(//node)[1]选择文档中的所有节点，然后只获取其中的第一个节点
例如：
```log
>>>from scrapy import Selector
>>>sel = Selector(text="""
....:     <ul class="list">
....:         <li>1</li>
....:         <li>2</li>
....:         <li>3</li>
....:     </ul>
....:     <ul class="list">
....:         <li>4</li>
....:         <li>5</li>
....:         <li>6</li>
....:     </ul>""")
>>>xp = lambda x: sel.xpath(x).getall()   此时xp是一个匿名方法，所以xp()是调用赋给xp的lambda匿名方法，并将参数传给 xp中lambda表达式中的x参数，返回结果
第一种：
这将获取其父项下的所有第一个＜li＞元素
>>>xp("//li[1]")
['<li>1</li>', '<li>4</li>']

第二种：
这将得到整个文档中的第一个＜li＞元素
>>>xp("(//li)[1]")
['<li>1</li>']

第三种：
这将获取＜ul＞父项下的所有第一个＜li＞元素
>>>xp("//ul/li[1]")
['<li>1</li>', '<li>4</li>']

第四种：
这将获得整个文档中＜ul＞父项下的第一个＜li＞元素
>>>xp("(//ul/li)[1]")
['<li>1</li>']
```

4.区分 xpath中的参数，经过string() 和 没经过转化的区别：
这个好难理解，例子如下：
当需要将文本内容用作XPath字符串函数的参数时，请避免使用//text（）并仅使用.代替
这是因为表达式//text（）生成文本元素的集合–一个节点集
当一个节点集被转换为字符串时，当它作为参数传递给一个字符串函数
（如contains（）或starts-with（））时，它只会生成第一个元素的文本。
例子：
```log
>>>from scrapy import Selector 
>>>sel=Selector(text='<a href=“#”>单击此处转到<strong>下一页</strong></a>'）
# 将节点集转换为字符串：
>>>sel.xpath('//a//text()').getall() # take a peek at the node-set
['Click here to go to the ', 'Next Page']
>>>sel.xpath("string(//a[1]//text())").getall() # convert it to string
['Click here to go to the ']
#然而，转换为字符串的节点将其自身及其所有子节点的文本组合在一起
>>>sel.xpath("//a[1]").getall() # 选择第一个节点
['<a href="#">Click here to go to the <strong>Next Page</strong></a>']
>>>sel.xpath("string(//a[1])").getall() # 将其转换为字符串
['Click here to go to the Next Page']
#因此，使用//text（）节点集在这种情况下不会选择任何内容：
sel.xpath("//a[contains(.//text(), 'Next Page')]").getall()
[ ]
#但使用 . 指节点，有效
>>>sel.xpath("//a[contains(., 'Next Page')]").getall()
['<a href="#">Click here to go to the <strong>Next Page</strong></a>']

注意：
即：再查找 当前元素集中是否包含某个字符串，可以通过contains(.,'字符串')来获得
```

5.XPath表达式中的变量
例如：
```log
#下面是一个基于元素的“id”属性值匹配元素的示例，不需要对其进行硬编码（如前所示）：
>>>response.xpath('//div[@id=$val]/a/text()', val='images').get()
'Name: My image 1 '
#下面是另一个示例，用于查找包含五个＜a＞子项的＜div＞标记的“id”属性（这里我们将值5作为整数传递）
>>>response.xpath('//div[count(a)=$cnt]/@id', cnt=5).get()
'images'
```

6.正在删除命名空间（没搞清）
在处理scrapy项目时，通常很方便地完全去掉名称空间，
只使用元素名称，编写更简单/方便的XPaths。
为此，可以使用Selector.remove_namespaces()方法。

7.扩展（没搞清）
正则表达式扩展
set扩展
（注意：这些扩展是指书写在 xpath括号中的）

8.其他扩展
has_class扩展（但：这个扩展，仅限在css无法描述的情况下使用，因为使用这个比较慢 效率低）
例如：
```python
<p class="foo bar-baz">First</p>
<p class="foo">Second</p>
<p class="bar">Third</p>
<p>Fourth</p>
可以这样使用：
>>>response.xpath('//p[has-class("foo")]')
[<Selector xpath='//p[has-class("foo")]' data='<p class="foo bar-baz">First</p>'>,
 <Selector xpath='//p[has-class("foo")]' data='<p class="foo">Second</p>'>]
>>>response.xpath('//p[has-class("foo", "bar-baz")]')
[<Selector xpath='//p[has-class("foo", "bar-baz")]' data='<p class="foo bar-baz">First</p>'>]
>>>response.xpath('//p[has-class("foo", "bar")]')
[]
```

9.查看地址：
https://doc.scrapy.org/en/latest/topics/selectors.html#topics-selectors-htmlcode
查看 最后的总结即可 （总结  可以帮助复习）


#### re获取数据的方式

1.使用re正则表达式提取数据 例如：（除了 re 还可以使用 getall get 提取数据）
```log
>>>response.css('title::text').re(r'Quotes.*')
['Quotes to Scrape']
>>>response.css('title::text').re(r'Q\w+')
['Quotes']
>>>response.css('title::text').re(r'(\w+) to (\w+)')
['Quotes', 'Scrape']
```

2.介绍re()  re_first()
re()获取所有匹配的字符串 
re_first()获取第一个匹配的字符串


#### 区分这三种提取方式

##### 区分css xpath re 三种方式

1.获取属性上：
css中：::attr(name)
xpath中:  @name
(name 代表属性名称)

2.re 与 css 、xpath提取数据的时候，是否能嵌套
css xpath在使用get() getall() re()之前，都能嵌套，使用之后，便不能进行嵌套
（使用它们之后，返回的结果都不再是 Selector类型，get()返回的是字符串 getall()返回的是字符串列表 re()返回的是字符串列表）

3.它们都可以相互使用，例如：css xpath
```log
>>>from scrapy import Selector
>>>sel = Selector(text='<div class="hero shout"><time datetime="2014-07-23 19:00">Special date</time></div>')
>>>sel.css('.shout').xpath('./time/@datetime').getall()
['2014-07-23 19:00']
```

### scrapy提取数据案例介绍

1.现在让我们来看看我们的spider被修改为递归地跟随链接到下一页，从中提取数据，代码如何书写吧
例如；
```python
# 导入模块
import scrapy
# 书写spider类
class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        'https://quotes.toscrape.com/page/1/',
    ]

    def parse(self, response):
        for quote in response.css('div.quote'):
            yield {
                'text': quote.css('span.text::text').get(),
                'author': quote.css('small.author::text').get(),
                'tags': quote.css('div.tags a.tag::text').getall(),
            }	#将数据返回，用于输出到文件中或数据库中

        next_page = response.css('li.next a::attr(href)').get() # 获取下一个链接的URL地址
        if next_page is not None:	# 如果有下一个链接的URL地址，则将 url地址 通过urljoin进行转换为路径，并将路径url再次传给parse进行解析并获取数据
            next_page = response.urljoin(next_page)
            yield scrapy.Request(next_page, callback=self.parse)
```

除了这样书写， 还可以通过一些快捷方法进行书写（作为创建请求对象的快捷方式，您可以使用response.follow）
例如：
```python
import scrapy
class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        'https://quotes.toscrape.com/page/1/',
    ]

    def parse(self, response):
        for quote in response.css('div.quote'):
            yield {
                'text': quote.css('span.text::text').get(),
                'author': quote.css('span small::text').get(),
                'tags': quote.css('div.tags a.tag::text').getall(),
            }

        next_page = response.css('li.next a::attr(href)').get()
        if next_page is not None:
            yield response.follow(next_page, callback=self.parse)     # 就是这里，对比上面，是不是少些了一行代码
结论：与scrapy.Request不同，response.follow直接支持相对URL-无需调用urljoin。注意response.follow只返回一个Request实例；您仍然必须yield此请求
(也就是 scrapy.Request()创建请求需要绝对路径，所以需要urljoin进行转换，response.follow支持相对路径，所以直接书写即可)
```

2.response.follow的更为精简用法：
```
(1).您也可以将选择器传递给response.follow而不是字符串；该选择器应提取必要的属性：
for href in response.css('ul.pager a::attr(href)'):
    yield response.follow(href, callback=self.parse)
(2).对于<a>元素，有一个快捷方式：response.follow自动使用其href属性。因此，代码可以进一步缩短：
for a in response.css('ul.pager a'):
    yield response.follow(a, callback=self.parse)
(3).要从可迭代对象创建多个请求，可以改用response.follow_all
anchors = response.css('ul.pager a')
yield from response.follow_all(anchors, callback=self.parse)
这样就更为简便了，或者进一步缩短：
yield from response.follow_all(css='ul.pager a', callback=self.parse)
```

3.下面是另一个spider，它展示了回调和以下链接，这次是为了抓取作者信息：
例如：
```python
# 导入模块
import scrapy
# 创建spider类
class AuthorSpider(scrapy.Spider):
    name = 'author'

    start_urls = ['https://quotes.toscrape.com/']

    def parse(self, response):
        author_page_links = response.css('.author + a')
        yield from response.follow_all(author_page_links, self.parse_author)	# 这个地方，是一个比较灵活的地方  等待当前页面获取完之后，继续获取下一页的内容

        pagination_links = response.css('li.next a')
        yield from response.follow_all(pagination_links, self.parse)

    def parse_author(self, response):
        def extract_with_css(query):
            return response.css(query).get(default='').strip()

        yield {
            'name': extract_with_css('h3.author-title::text'),
            'birthdate': extract_with_css('.author-born-date::text'),
            'bio': extract_with_css('.author-description::text'),
        }
```

4.参数传递（通过 cb_kwargs 进行传递）
例如：
```python
def parse(self, response):
    request = scrapy.Request('http://www.example.com/index.html',
                             callback=self.parse_page2,
                             cb_kwargs=dict(main_url=response.url))
    request.cb_kwargs['foo'] = 'bar'   	# 为回调添加更多参数
    yield request

def parse_page2(self, response, main_url, foo):
    yield dict(
        main_url=main_url,
        other_url=response.url,
        foo=foo,
    )
注意：
Request.cb_kwargs是在1.7版中引入的。在此之前，建议使用Request.meta传递回调信息
1.7之后，Request.cb_kwargs成为处理用户信息的首选方式，留下Request.meta与中间件和扩展等组件进行通信
```


### scrapy提取数据时 传参的案例介绍

使用spider参数：
1.运行spider时，可以使用-a选项为其提供命令行参数：
scrapy crawl quotes -O quotes-humor.json -a tag=humor
这些参数传递给Spider的__init__方法，默认情况下成为Spider属性，
在本例中，为标记参数提供的值将通过self.tag提供。
您可以使用此选项使spider仅获取带有特定标记的引号，并根据参数构建URL：
例如：
```python
# 导入模块
import scrapy
# 书写 spider类
class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        url = 'https://quotes.toscrape.com/'
        tag = getattr(self, 'tag', None)	# 在这里获取命令行中给到的参数和值（如果没有给到tag 则赋值一个默认值None）
        if tag is not None:
            url = url + 'tag/' + tag
        yield scrapy.Request(url, self.parse)

    def parse(self, response):
        for quote in response.css('div.quote'):
            yield {
                'text': quote.css('span.text::text').get(),
                'author': quote.css('small.author::text').get(),
            }

        next_page = response.css('li.next a::attr(href)').get()
        if next_page is not None:
            yield response.follow(next_page, self.parse)
```
注意：
如果将tag=human参数传递给这个spider，
您会注意到它只会访问来自human标记的URL，例如https://quotes.toscrape.com/tag/humor.

2.详细介绍：
(1).spider可以接受修改其行为的参数。
spider参数的一些常见用法是定义起始URL或将爬网限制到站点的某些部分，
但它们可以用于配置spider的任何功能
(2).spider参数使用-a选项通过爬网命令传递。例如：
>scrapy crawl myspider -a category=electronics
spider可以访问__init__方法中的参数：
代码如下：
```python
import scrapy
class MySpider(scrapy.Spider):
    name = 'myspider'

    def __init__(self, category=None, *args, **kwargs):
        super(MySpider, self).__init__(*args, **kwargs)
        self.start_urls = [f'http://www.example.com/categories/{category}']
......
```

更多可以参考：
https://doc.scrapy.org/en/latest/intro/tutorial.html#more-examples-and-patterns
中的教程


### 介绍scrapy item 数据项的创建使用

一.创建item类的方法：
第一种：
```python
from scrapy.item import Item, Field

class CustomItem(Item):
    one_field = Field()
    another_field = Field()

第二种：
from dataclasses import dataclass

@dataclass
class CustomItem:
    one_field: str
    another_field: int

注意：在运行时不强制执行字段类型。

第三种：
import attr

@attr.s
class CustomItem:
    one_field = attr.ib()
    another_field = attr.ib()

注意：为了使用这种类型，需要安装attrs软件包。

第四种：
import scrapy

class Product(scrapy.Item):
    name = scrapy.Field()
    price = scrapy.Field()
    stock = scrapy.Field()
    tags = scrapy.Field()
    last_updated = scrapy.Field(serializer=str)

注意：熟悉Django的人会注意到，Scrapy Items的定义与Django模型类似，
只是Scrapy Item要简单得多，因为没有不同字段类型的概念。
```

二.使用Item：
1.创建item
```
>>> product = Product(name='Desktop PC', price=1000)
>>>print(product)
Product(name='Desktop PC', price=1000)
```

2.获取字段值
```log
>>> product['name']
Desktop PC
>>> product.get('name')
Desktop PC
正常输出

>>> product['price']
1000
正常输出

>>> product['last_updated']
Traceback (most recent call last):
    ...
KeyError: 'last_updated'
未赋值，无法取到值，所以报错

>>> product.get('last_updated', 'not set')
not set
未赋值，但给了一个 not set 默认值

>>> product['lala'] # getting unknown field
Traceback (most recent call last):
    ...
KeyError: 'lala'
未在item类中定义，所以报错

>>> product.get('lala', 'unknown field')
'unknown field'
未在item类中定义，但给了一个unknown field默认值

>>> 'name' in product  # is name field populated?
True
在创建item的时候，赋了值，所以为true

>>> 'last_updated' in product  # is last_updated populated?
False
在创建item的时候，没有赋值，所以为false

>>> 'last_updated' in product.fields  # is last_updated a declared field?
True
在item中有定义，则输出true

>>> 'lala' in product.fields  # is lala a declared field?
False
在item中没定义，则输出false
```

3.设置字段的值
```log
>>> product['last_updated'] = 'today'
>>> product['last_updated']
today
>>> product['lala'] = 'test' # setting unknown field
Traceback (most recent call last):
    ...
KeyError: 'Product does not support field: lala'
```

4.访问所有赋了值的字段值
要访问所有填充的值，只需使用传统的api  （使用python中的dict类型进行访问就行）：
```log
>>> product.keys()
['price', 'name']
>>> product.items()
[('price', 1000), ('name', 'Desktop PC')]
```

5.复制 item
要复制项目，必须首先决定是浅层复制还是深层复制。

如果您的项包含列表或字典之类的可变值，
那么浅拷贝将在所有不同的拷贝中保留对相同可变值的引用。

例如，如果您有一个带有标记列表的项目，并且您创建了该项目的浅副本，则原始项目和副本都具有相同的标记列表。
将标签添加到其中一个项目的列表中，也会将该标签添加到另一个项目中。
如果这不是所需的行为，请使用深度复制。

要创建项的浅层副本，可以对现有项调用copy()（product2=product.copy() ），
也可以从现有项实例化项类（product2=Product(product) ）。

要创建深度复制，请改为调用deepcopy()（product2=product.deepcopy() ）。

6.其他常见任务
正在根据项创建dicts：
```log
>>> dict(product) # create a dict from all populated values
{'price': 1000, 'name': 'Desktop PC'}

正在从dicts创建项目：
>>> Product({'name': 'Laptop PC', 'price': 1500})
Product(price=1500, name='Laptop PC')
>>> Product({'name': 'Laptop PC', 'lala': 1500}) # warning: unknown field in dict
Traceback (most recent call last):
    ...
KeyError: 'Product does not support field: lala'
```

7.扩展项目子类
您可以通过声明原始Item的子类来扩展Items（添加更多字段或更改某些字段的元数据）。
例如：
```python
class DiscountedProduct(Product):
    discount_percent = scrapy.Field(serializer=str)
    discount_expiration_date = scrapy.Field()
```

您还可以通过使用以前的字段元数据来扩展字段元数据，并添加更多值，或更改现有值，如下所示：
```python
class SpecificProduct(Product):
    name = scrapy.Field(Product.fields['name'], serializer=my_serializer)
```
这将添加（或替换）name字段的rializermetadata键，保留所有以前存在的元数据值。

8.支持所有项目类型
```log
在接收项目的代码中，例如项目管道或pider中间件的方法，
最好使用 ItemAdapter class和 is_item（）函数来编写适用于支持的项目类型的代码：
class itemadapter.ItemAdapter(item:Any) [source]
用于与数据容器对象交互的包装器类。
它提供了一个通用接口来提取和设置数据，而不必考虑对象的类型。

itemadapter.is_item(obj:Any)→bool [source]
如果给定对象属于支持的类型之一，则返回True，否则返回False。
ItemAdapter.is_item的别名
```

9.与项目相关的其他类别
```python
class scrapy.item.ItemMeta(class_name,bases,attrs) [source]
```
处理字段定义的元素的元类。

10.Item loader 项目加载器（扩展）
例如：
```python
from scrapy.loader import ItemLoader
from myproject.items import Product

def parse(self, response):
    l = ItemLoader(item=Product(), response=response)
    l.add_xpath('name', '//div[@class="product_name"]')
    l.add_xpath('name', '//div[@class="product_title"]')
    l.add_xpath('price', '//p[@id="price"]')
    l.add_css('stock', 'p#stock')
    l.add_value('last_updated', 'today') # you can also use literal values
    return l.load_item()
```

(1)Dataclass的方式创建：
```python
from dataclasses import dataclass, field
from typing import Optional

@dataclass
class InventoryItem:
    name: Optional[str] = field(default=None)
    price: Optional[float] = field(default=None)
    stock: Optional[int] = field(default=None)
```
使用过程：
```python
l = ItemLoader(Product(), some_selector)
l.add_xpath('name', xpath1) # (1)
l.add_xpath('name', xpath2) # (2)
l.add_css('name', css) # (3)
l.add_value('name', 'test') # (4)
return l.load_item() # (5)
```


(2)Declaring Item Loaders
项加载器是使用类定义语法声明的。以下是一个示例：
```python
from itemloaders.processors import TakeFirst, MapCompose, Join
from scrapy.loader import ItemLoader

class ProductLoader(ItemLoader):

    default_output_processor = TakeFirst()

    name_in = MapCompose(str.title)
    name_out = Join()

    price_in = MapCompose(str.strip)

    # ...
```
注意：正如您所看到的，输入处理器是使用_in后缀声明的，而输出处理器是使用_out后缀声明的。
还可以使用ItemLoader.default_input_processor和ItemLoader.default _output_procprocessor属性声明默认输入/输出处理器。

声明输入和输出处理器：
如前一节所示，输入和输出处理器可以在ItemLoader定义中声明，并且以这种方式声明输入处理器是非常常见的。
但是，还有一个地方可以指定要使用的输入和输出处理器：在项目字段元数据中。以下是一个示例：
```python
import scrapy
from itemloaders.processors import Join, MapCompose, TakeFirst
from w3lib.html import remove_tags

def filter_price(value):
    if value.isdigit():
        return value

class Product(scrapy.Item):
    name = scrapy.Field(
        input_processor=MapCompose(remove_tags),
        output_processor=Join(),
    )
    price = scrapy.Field(
        input_processor=MapCompose(remove_tags, filter_price),
        output_processor=TakeFirst(),
    )
```
```log
>>> from scrapy.loader import ItemLoader
>>> il =ItemLoader(item=Product())
>>> il.add_value('name', ['Welcome to my', '<strong>website</strong>'])
>>> il.add_value('price', ['&euro;', '<span>1000</span>'])
>>> il.load_item()

{'name': 'Welcome to my website', 'price': '1000'}
```

输入和输出处理器的优先顺序如下：
  项目加载器字段特定属性：field_in和field_out（最高优先级）
  字段元数据（输入_处理器和输出_处理器密钥）
  项目加载器默认值：ItemLoader.default_input_processor（）和ItemLoader.default _output_proccessor（）（优先级最低）

另请参阅：重用和扩展Item Loader。[`去看看`](https://doc.scrapy.org/en/latest/topics/loaders.html#topics-loaders-extending)


11.项目加载器上下文
项目加载器上下文是在项目加载器中的所有输入和输出处理器之间共享的任意键/值的dict。
它可以在声明、实例化或使用项加载器时传递。它们用于修改输入/输出处理器的行为。
例如，假设您有一个函数parse_length，它接收一个文本值并从中提取一个长度：
```python
def parse_length(text, loader_context):
    unit = loader_context.get('unit', 'm')
    # ... length parsing code goes here ...
    return parsed_length
```
通过接受loader_context参数，该函数明确地告诉Item loader它能够接收Item loader上下文，
因此Item loader在调用它时传递当前活动的上下文，因此处理器函数（在本例中为parse_length）可以使用它们。
有几种方法可以修改Item Loader上下文值：
通过修改当前活动的Item Loader上下文（上下文属性）：
```python
loader = ItemLoader(product)
loader.context['unit'] = 'cm'
```
在项目加载器实例化时
(项目加载器__init__方法的关键字参数存储在项目加载器上下文中）：
```python
loader = ItemLoader(product, unit='cm')
```
在ItemLoader声明中，对于那些支持使用ItemLoader上下文实例化它们的输入/输出处理器。
MapCompose就是其中之一：
```python
class ProductLoader(ItemLoader):
    length_out = MapCompose(parse_length, unit='cm')
```

ItemLoader对象:
```python
class scrapy.loader.ItemLoader(item=None, selector=None, response=None, parent=None, **context) [source]
```

```
一种用户友好的抽象，通过将字段处理器应用于抓取的数据来用数据填充项目。
当使用选择器或响应进行实例化时，它支持使用选择器从网页中提取数据。
参数
item（scrapy.item.item）– 要使用对add_xpath（）、add_css（）或add_value（）的后续调用填充的项实例。
selector（selector对象）– 当使用add_xpath（）、add_css（）、replace_xpath[（）或replace_css（]方法时，要从中提取数据的选择器。
response（response对象）– 用于使用default_selector_class构造选择器的响应，除非给定了选择器参数，在这种情况下会忽略此参数。

如果没有给定项，则会使用default_item_class中的类自动实例化一个项。
项、选择器、响应和剩余的关键字参数被分配给Loader上下文（可通过上下文属性访问）。
```


### 介绍 pipeline 管道的创建使用

在pipeline.py中创建管道文件，该文件在 创建item的时候，同步进行（前提需要在 settings.py中配置item_pipeline）
学习pipeline
https://doc.scrapy.org/en/latest/topics/item-pipeline.html

一.Pipeline数据管道
在一个项目被scrapy刮取后，它被发送到项目管道，该管道通过顺序执行的几个组件来处理它。
每个项目管道组件（有时仅称为“项目管道”）都是一个实现简单方法的Python类。他们接收一个项目并对其执行操作，
同时决定该项目是应该继续通过管道，还是被丢弃并不再处理。

数据管道的典型用途有：
  清除HTML数据
  验证抓取的数据（检查项目是否包含某些字段）
  检查重复项（并删除它们）
  将刮掉的项目存储在数据库中

1.编写自己的项目管道
每个项管道组件都是一个Python类，必须实现以下方法：
(1)process_item(self, item, spider）
此方法是为每个项目管道组件调用的。
item是一个item对象，请参阅支持所有item类型。
process_item（）必须：返回项对象、返回Deferred或引发DropItem异常中一个。
丢弃的项目不再由其他管道组件处理。
参数项目（item对象）-scraped 项目
spider（scrapy对象）–scraped item 的scrapy

(2)open_spider(self, spider)
当spider打开时会调用此方法。
参数 spider(spider对象）–打开的spider

(3)close_spider(self, spider)¶
当spider关闭时调用此方法。
参数 spider(spider对象）–已关闭的spider

(4)classmethodfrom_crawler(cls, crawler)
如果存在，则调用此类方法以从爬网程序创建管道实例。它必须返回管道的一个新实例。
Crawler对象提供对所有Scrapy核心组件的访问，如设置和信号；这是管道访问它们并将其功能挂接到Scrapy的一种方式。
参数 crawler (Crawler object) –使用此管道的爬网程序

2.项目管道示例
价格验证和取消没有价格的项目
让我们看看下面的假设管道，它调整那些不包括增值税的项目的价格属性（price_excludes_VAT属性），
并删除那些不包含价格的项目：
```python
from itemadapter import ItemAdapter
from scrapy.exceptions import DropItem

class PricePipeline:
    vat_factor = 1.15

    def process_item(self, item, spider):
        adapter = ItemAdapter(item)
        if adapter.get('price'):
            if adapter.get('price_excludes_vat'):
                adapter['price'] = adapter['price'] * self.vat_factor
            return item
        else:
            raise DropItem(f"Missing price in {item}")
```

3.将项目写入JSON行文件
以下管道将所有抓取的项（来自所有蜘蛛）存储到一个items.jsonl文件中，每行包含一个以JSON格式序列化的项：
```python
import json

from itemadapter import ItemAdapter

class JsonWriterPipeline:

    def open_spider(self, spider):
        self.file = open('items.jsonl', 'w')

    def close_spider(self, spider):
        self.file.close()

    def process_item(self, item, spider):
        line = json.dumps(ItemAdapter(item).asdict()) + "\n"
        self.file.write(line)
        return item
```
JsonWriterPipeline的目的只是介绍如何编写项目管道。
如果您真的想将所有抓取的项目存储到JSON文件中，那么应该使用Feed导出。[`去看看`](https://doc.scrapy.org/en/latest/topics/feed-exports.html#topics-feed-exports)

4.将项目写入MongoDB
在这个例子中，我们将使用pymongo将项目写入MongoDB。
MongoDB地址和数据库名称在Scrapy设置中指定；MongoDB集合以项类命名。
这个例子的要点是展示如何使用from_crawler() 方法以及如何正确清理资源

```python
import pymongo
from itemadapter import ItemAdapter

class MongoPipeline:

    collection_name = 'scrapy_items'

    def __init__(self, mongo_uri, mongo_db):
        self.mongo_uri = mongo_uri
        self.mongo_db = mongo_db

    @classmethod
    def from_crawler(cls, crawler):
        return cls(
            mongo_uri=crawler.settings.get('MONGO_URI'),
            mongo_db=crawler.settings.get('MONGO_DATABASE', 'items')
        )

    def open_spider(self, spider):
        self.client = pymongo.MongoClient(self.mongo_uri)
        self.db = self.client[self.mongo_db]

    def close_spider(self, spider):
        self.client.close()

    def process_item(self, item, spider):
        self.db[self.collection_name].insert_one(ItemAdapter(item).asdict())
        return item
```

5.拍摄项目的屏幕截图
这个例子演示了如何在process_item（）方法中使用协程语法。
这个项目管道向本地运行的Splash实例发出请求，以呈现项目URL的屏幕截图。
下载请求响应后，项目管道将屏幕截图保存到一个文件中，并将文件名添加到项目中。
```python
import hashlib
from pathlib import Path
from urllib.parse import quote

import scrapy
from itemadapter import ItemAdapter
from scrapy.http.request import NO_CALLBACK
from scrapy.utils.defer import maybe_deferred_to_future


class ScreenshotPipeline:
    """Pipeline that uses Splash to render screenshot of
    every Scrapy item."""

    SPLASH_URL = "http://localhost:8050/render.png?url={}"

    async def process_item(self, item, spider):
        adapter = ItemAdapter(item)
        encoded_item_url = quote(adapter["url"])
        screenshot_url = self.SPLASH_URL.format(encoded_item_url)
        request = scrapy.Request(screenshot_url, callback=NO_CALLBACK)
        response = await maybe_deferred_to_future(
            spider.crawler.engine.download(request, spider)
        )

        if response.status != 200:
            # Error happened, return item.
            return item

        # Save screenshot to file, filename will be hash of url.
        url = adapter["url"]
        url_hash = hashlib.md5(url.encode("utf8")).hexdigest()
        filename = f"{url_hash}.png"
        Path(filename).write_bytes(response.body)

        # Store filename in item.
        adapter["screenshot_filename"] = filename
        return item
```

6.重复筛选器(filter)
一个筛选器，用于查找重复的项目，并删除已处理的项目。
假设我们的物品有一个唯一的id，但我们的spider返回多个具有相同id的物品：
```python
from itemadapter import ItemAdapter
from scrapy.exceptions import DropItem

class DuplicatesPipeline:

    def __init__(self):
        self.ids_seen = set()

    def process_item(self, item, spider):
        adapter = ItemAdapter(item)
        if adapter['id'] in self.ids_seen:
            raise DropItem(f"Duplicate item found: {item!r}")
        else:
            self.ids_seen.add(adapter['id'])
            return item
```

7.激活项目管道组件
要激活项目管道组件，必须将其类添加到Item_PIPELINES设置中，如以下示例所示：
```python
ITEM_PIPELINES = {
    'myproject.pipelines.PricePipeline': 300,
    'myproject.pipelines.JsonWriterPipeline': 800,
}
```
在此设置中分配给类的整数值决定了它们运行的顺序：
项从值较低的类到值较高的类。
通常将这些数字定义在0-1000范围内。
