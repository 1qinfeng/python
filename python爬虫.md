# **使用HTTPPasswordMgrWithDefaultRealm,HTTPBasicAuthHandler,build_opener库来进行模拟用户登录**

'''导入*HTTPPasswordMgrWithDefaultRealm、HTTPBasicAuthHandler、build_opener库*来进行模拟登录'''
~~~python
from urllib.request import HTTPPasswordMgrWithDefaultRealm,HTTPBasicAuthHandler,build_opener

from urllib.error import URLError

#设置基本参数：url、user-name、password等

url=input('访问的地址：')

username=input('账号：')

password=input('密码：')

'''首先，实例化一个HTTPPasswordMgrWithDefaultRealm对象auth-handler其参数是HTTPPasswordMgrWithDefaultRealm对象，利用add_password方法来添加用户账号和密码，这样就建立起一个用于处理验证的handler类'''

p=HTTPPasswordMgrWithDefaultRealm()

p.add_password(None,url,username,password)

auth_handler=HTTPBasicAuthHandler(p)

'''将刚建立的auth-hander作为参数传入build-opener方法中，构建一个opener，用于发送请求'''

opener=build_opener(auth_handler)

'''完成验证。获取源码；若未成功，输出原因'''

try:

	result=opener.open(url)

	print(result.read().decode())

except URLError as e:

	print(e.reason)
~~~
# **设置代理**

做爬虫时免不了要使用代理，因为可能*被封IP*

设置代理如下：
~~~python
'''导入ProxyHandler、build_opener库来进行模拟代理'''

from urllib.request import ProxyHandler,build_opener

from urllib.error import URLError

#设置基本参数：url

url=input('访问的地址：')

'''首先，构建一个本地HTTP代理运行在7890端口上，

ProxyHandler其参数是一个字典key为协议名，value是代理链接'''

proxy_handler=ProxyHandler({

'http':'http://127.0.0.1:7890',

'https':'https://127.0.0.1:7890'

})

'''将刚建立的proxy_handler作为参数传入build-opener方法中，构建一个opener，用于发送请求'''

opener=build_opener(proxy_handler)

'''完成验证。获取源码；若未成功，输出原因'''

try:

	result=opener.open(url)
	
	print(result.read().decode())

except URLError as e:

	print(e.reason)
~~~
# **cookie**

获取cookie
~~~python
'''导入http.cookiejar库'''

import http.cookiejar,urllib.request

#设置参数

url=input('请求网址：')

cookie=http.cookiejar.CookieJar()

handler=urllib.request.HTTPCookieProcessor(cookie)

opener=urllib.request.build_opener(handler)

response=opener.open(url)

for item in cookie:

	print(item.name+'='+item.value)
~~~
保存cookie
~~~python
#这一行导入了urllib.request允许Python代码发出HTTP请求的模块，以及http.cookiejar提供对处理cookie的支持的模块。

import urllib.request,http.cookiejar

#提示用户输入一个URL以将HTTP请求发送到并将输入存储在变量中url。

url=input('请输入请求网址：')

#设置要保存的cookie文件的文件名为“cookie.txt”。

filename='cookie.txt'

#创建了一个名为的新MozillaCookieJar对象cookie，它将存储从服务器接收到的cookie。

cookie=http.cookiejar.MozillaCookieJar(filename)

#创建了一个HTTPCookieProcessor名为的对象handler，它将处理从服务器接收到的cookie并将它们存储在该cookie对象中。

handler=urllib.request.HTTPCookieProcessor(cookie)

#创建一个OpenerDirector名为的对象opener，它将用于打开URL并使用该handler对象发送HTTP请求。

opener=urllib.request.build_opener(handler)

#向用户指定的URL发送HTTP请求，并将响应存储在对象中response。

response=opener.open(url)

#将从服务器接收到的cookies保存到变量指定的文件中filename，忽略任何被标记为“丢弃”或已经过期的cookies。

cookie.save(ignore_discard=True,ignore_expires=True)
~~~
> 运行结果
>
 	[https://www.baidu.com](https://www.baidu.com)
		
		cookie.txt:
	
	#NetscapeHTTPCookieFile
	
	#http://curl.haxx.se/rfc/cookie_spec.html
	
	#Thisisageneratedfile!Donotedit.
	
	[www.baidu.comFALSE/FALSE1683384806BD_NOT_HTTPS1](http://www.baidu.comFALSE/FALSE1683384806BD_NOT_HTTPS1)
	
	.baidu.comTRUE/FALSE3830868153BIDUPSID3B0AF647BDC8C19C97B977B0D186245E
	
	.baidu.comTRUE/FALSE3830868153PSTM1683384507
	
	.baidu.comTRUE/FALSE1714920506BAIDUID3B0AF647BDC8C19C46BF0A442CA4882E:FG=1

以LWP格式保存
~~~python
#这一行导入了urllib.request允许Python代码发出HTTP请求的模块，以及http.cookiejar提供对处理cookie的支持的模块。

import urllib.request,http.cookiejar

#提示用户输入一个URL以将HTTP请求发送到并将输入存储在变量中url。

url=input('请输入请求网址：')

#设置要保存的cookie文件的文件名为“cookie.txt”。

filename='cookie.txt'

#创建了一个名为的新MozillaCookieJar对象cookie，它将存储从服务器接收到的cookie。

cookie=http.cookiejar.LWPCookieJar(filename)

#创建了一个HTTPCookieProcessor名为的对象handler，它将处理从服务器接收到的cookie并将它们存储在该cookie对象中。

handler=urllib.request.HTTPCookieProcessor(cookie)

#创建一个OpenerDirector名为的对象opener，它将用于打开URL并使用该handler对象发送HTTP请求。

opener=urllib.request.build_opener(handler)

#向用户指定的URL发送HTTP请求，并将响应存储在对象中response。

response=opener.open(url)

#将从服务器接收到的cookies保存到变量指定的文件中filename，忽略任何被标记为“丢弃”或已经过期的cookies。

cookie.save(ignore_discard=True,ignore_expires=True)
~~~
> 运行结果
	[https://www.baidu.com](https://www.baidu.com)
	
	
	
	#LWP-Cookies-2.0
	
	Set-Cookie3:BD_NOT_HTTPS=1;path="/";domain="www.baidu.com";path_spec;expires="2023-05-0615:02:24Z";version=0
	
	Set-Cookie3:BIDUPSID=4906C0440B31B78F6BC35C1723C0B1B0;path="/";domain=".baidu.com";path_spec;domain_dot;expires="2091-05-2418:11:31Z";version=0
	
	Set-Cookie3:PSTM=1683385045;path="/";domain=".baidu.com";path_spec;domain_dot;expires="2091-05-2418:11:31Z";version=0
	
	Set-Cookie3:BAIDUID="4906C0440B31B78F3EA62186E3B11140:FG=1";path="/";domain=".baidu.com";path_spec;domain_dot;expires="2024-05-0514:57:24Z";comment=bd;version=0
利用cookie：
~~~python
#导入了urllib.request允许Python代码发出HTTP请求的模块，以及http.cookiejar提供对处理cookie的支持的模块。

import urllib.request,http.cookiejar

url=input('请输入网址：')

#这一行创建了一个LWPCookieJar名为的新对象cookie，它将用于存储从服务器接收到的cookie。

cookie=http.cookiejar.LWPCookieJar()

#从filename指定的文件加载cookiecookie.txt，忽略任何已标记为“丢弃”或已过期的cookie。

cookie.load('cookie.txt',ignore_discard=True,ignore_expires=True)

#创建了一个HTTPCookieProcessor名为的对象handler，它将处理从服务器接收到的cookie并将它们存储在该cookie对象中。

handler=urllib.request.HTTPCookieProcessor(cookie)

#创建一个OpenerDirector名为的对象opener，它将用于打开URL并使用该handler对象发送HTTP请求。

opener=urllib.request.build_opener(handler)

#向用户指定的URL发送HTTP请求，并将响应存储在对象中responer。

responer=opener.open(url)

#此行将HTTP响应的内容打印为字符串，将其从字节解码为UTF-8格式

print(responer.read().decode('utf-8'))
~~~
4、处理异常

**URLError:**

是urllib库的error模块，是error异常模块的基类，由request模块产生的异常都可以通过捕获此类来处理。有一个属性reason，即返回错误的原因。

**HTTPError**是URLError的一个子类，专门用来处理HTTP类的错误，有三个属性：
*code：返回状态码
Reason:返回错误的原因
headers：返回请求头*

**一般情况下，先捕获子类错误HTTPError,后返回父类错误URLError**
~~~python
#导入所需的模块：socket和urllib.error。

import socket

from urllib import request,error

#提示用户输入URL和超时值，分别存储在url和timeout变量中

url=input('请输入网址：')

timeout=float(input('设置响应时间：'))

#尝试使用urllib.request.urlopen()方法打开URL，并将超时参数设置为用户输入的值。如果请求成功，脚本将打印"RequestSuccessfully!"。

try:
	
	response=request.urlopen(url,timeout=timeout)
	
	#如果发生HTTP错误，脚本使用异常捕获错误，并打印错误代码、原因和头部信息。如果发生URL错误（例如无效的URL），脚本使用异常捕获错误，并打印原因。如果原因是套接字超时错误，脚本还会打印"timeout"

excepterror.HTTPError as e:

	print(e.reason,e.code,e.headers,sep='\n')

except error.URLError as e:

	print(e.reason,type(e.reason),sep='\n')
	
	if isinstance(e.reason,socket.timeout):
	
	print('timeout')
	
else:

	print('ResquestSuccessfully!')
~~~
# **综合运用**
~~~python
from urllib.request import HTTPPasswordMgrWithDefaultRealm,HTTPBasicAuthHandler,build_opener

import http.cookiejar

from random import*

import urllib.error

import socket

import urllib.request

url=input('请输入请求的网址：')

username=input('请输入账号：')

password=input('请输入密码：')

host=url[6:-1]

filename='cookie.txt'

user_agents=[

'Mozilla/5.0(Macintosh;U;IntelMacOSX10_6_8;en-us)AppleWebKit/534.50(KHTML,likeGecko)Version/5.1Safari/534.50',

'Mozilla/5.0(Windows;U;WindowsNT6.1;en-us)AppleWebKit/534.50(KHTML,likeGecko)Version/5.1Safari/534.50',

'Mozilla/5.0(compatible;MSIE9.0;WindowsNT6.1;Trident/5.0',

'Mozilla/5.0(WindowsNT6.1;rv:2.0.1)Gecko/20100101Firefox/4.0.1'

'Opera/9.80(WindowsNT6.1;U;en)Presto/2.8.131Version/11.11'

]

headers={
			
			'User-Agent':choice(user_agents),
			
			'Host':host
			
			}

p=HTTPPasswordMgrWithDefaultRealm()

p.add_password(None,url,username,password)

auth_handler=HTTPBasicAuthHandler()

cookie=http.cookiejar.LWPCookieJar(filename)

cookie_handler=urllib.request.HTTPCookieProcessor(cookie)

opener=build_opener(auth_handler,cookie_handler)

try:

	req=urllib.request.Request(url,headers=headers)
	
	response=urllib.request.urlopen(req),opener.open(url)
	
	print(response.read().decode())
	
	cookie.save(ignore_discard=True,ignore_expires=True)

except urllib.error.HTTPErrorase:

	print(e.reason,e.code,e.headers,sep='\n')

except urllib.error.URLError as e:

	print(e.reason)

if isinstance(e.reason,socket.timeout):

	print('TIMEOUT')
~~~
> 解释
这段代码实现了通过HTTP Basic认证方式登录指定的网页，并在登录成功后获取该网页返回的cookie信息。

代码主要的功能如下：

	1.  提示用户输入需要请求的网址、账号和密码。
	2.  从用户输入中解析出需要登录的网址、账号和密码，并创建一个HTTPPasswordMgrWithDefaultRealm对象，用于保存网站域名、用户名和密码的映射关系。
	3.  创建一个HTTPBasicAuthHandler对象，用于处理HTTP Basic认证。
	4.  创建一个LWPCookieJar对象，并将其与HTTPCookieProcessor对象配合使用，用于处理cookie。
	5.  创建一个OpenerDirector对象，并将上述的认证处理器和cookie处理器加入到该对象中，用于发送HTTP请求并处理HTTP响应。
	6.  随机选择一个User-Agent字符串，并将其添加到HTTP请求头中。
	7.  发送HTTP请求，如果HTTP请求成功，则输出响应的内容并保存cookie信息；如果HTTP请求失败，则输出错误信息。
	
	总的来说，这段代码通过HTTP Basic认证方式实现了登录指定的网页，并获取该网页返回的cookie信息，同时实现了随机更换User-Agent字符串的功能
	
	'''

# **解析链接**

urllib库中的*parse模块*，可以解析url

实例：
~~~python
from urllib.parse import urlparse

url=input('请输入要解析的网址：')

result=urlparse(url,allow_fragments=True)

print(type(result))

print(result)
~~~
> 运行结果：
	[https://mooc1.chaoxing.com/mycourse/studentstudy?chapterId=735381775&courseId=233780355&clazzid=75154229&enc=d40ed21616fe8c9bb81bf1ad4b40d818](https://mooc1.chaoxing.com/mycourse/studentstudy?chapterId=735381775&courseId=233780355&clazzid=75154229&enc=d40ed21616fe8c9bb81bf1ad4b40d818)
	
	
	
	<class 'urllib.parse.ParseResult'>
	
	ParseResult(scheme='https', netloc='mooc1.chaoxing.com', path='/mycourse/studentstudy', params='', query='chapterId=735381775&courseId=233780355&clazzid=75154229&enc=d40ed21616fe8c9bb81bf1ad4b40d818', fragment='')

**一个标准的链接格式：**
<span style="color:green">
Scheme://netloc/path:params?query?#fragment
Scheme:协议头
netloc：域名
path：访问路径
params：参数
Query:查询条件
fragment：直接定位页面内部的下拉位置
@urlparse的三个参数：
	<span style="color:red">1.  Urlstring:待解析的url
	2.  schemes：默认协议，如果待解析的url没有指明协议，则使用默认协议
	3.  allow_fragment:是否忽略fragment</span>
---
休息一下，看个抖音！
[抖音](https://www.douyin.com/)
学够了吗？来一张图片来养养眼
![[img (1).jpg]]
---
