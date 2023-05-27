# python标准库笔记

2023年5月10日

23:19

一、***string模块***

函数：

1、  **capword()**

用法：将字符串中每一个字符单词大写

例子：
~~~python
importstring

s='raoyangisafool!'

print(s)

print(string.capwords(s))
~~~

>	运行结果：

	rao yang is a fool!
	
	Rao Yang Is A Fool!

原理：先使用spilt()函数来拆分字符串，将所拆分的单个字符串一类表形式储存。然后大写字符串，后用join()函数组合。

---

2、**字符串模板**

_String.Template_、_使用操作符%_、_str.format（)_都可实现字符串模板化。

例子：
~~~python
importstring

values={'var':input('请输入value：')}

t=string.Template('''

Variable:$var

Escape:$$

Variableintext:${var}iable

''')

print('TEMPLATE:',t.substitute(values))

s='''

Variable:%(var)s

Escape:%%

Variableintext:%(var)siable

'''

print('INTERPOLATION:',s%values)

s='''

Variable:(var)

Escape:{{}}

Variableintext:{var}iable

'''

print('FORMAT:',s.format(**values))
~~~

>	运行结果：

	请输入value：rao
	
	TEMPLATE:
	
	Variable        :rao
	
	Escape          :$
	
	Variable in text:raoiable
	
	INTERPOLATION:
	
	Variable          :rao
	
	Escape            :%
	
	Variable in text  :raoiable
	
	FORMAT:
	
	Variable         :(var)
	
	Escape           :{}
	
	Variable in text :raoiable

* .  **String.Template字符串模板化**原理：

使用_$符号来引入定义的变量，若有必要区分与周围其他的文本时可以使用$(value)_来进行处理，**打印方式:print('自定义名：'，变量名.substitute（value）)**

* .  操作符%实现字符串模块化：

使用%符号来引入定义的变量，若有必要区分与周围其他的文本时可以使用%(value)来进行处理。打印方式：print('自定义名：'，变量名（一个空格）%（一个空格）values)

* .  Str.format()实现字符串模块化：

使用{}来作为占位符，在最后的打印时用str.format（）可在占位符中填充定义的变量。

---

3、**字符串模块化异常处理**：

     对于字符串模块中没有定义的变量，在返回值时会出现keyerror的报错，若使用safe_substitute(),这不会报错，会返回没有定义的变量。

例子：
~~~python
importstring

values={'var':'rao'}

t=string.Template("$varisa$fool!")

try:

print('substitute():',t.substitute(values))

exceptKeyErroraserr:

print('ERROR:',str(err))

print('safe_Substitute():',t.safe_substitute(values))
~~~
>	运行结果：

	ERROR: 'fool'
	
	safe_Substitute() : rao is a $fool !

从运行结果可知，由于没有fool定义的变量，所以返回值是依旧返回$fool。

---

4、**formatter**

与format用法相似。用于定义字符串的输出格式。其特性包括类型的强制转换、对齐、属性和域引用、命名和位置模块参数以及类型特定的格式化选项等。

5、**常量**

string模块包括大量的与ASCII和数字字符集相关的常量。

获取string模块的所有属性和方法：
~~~python
import string

impor tinspect

def is_str(value):

	return isinstance(value,str)
	
	forname,valueininspect.getmembers(string,is_str):
	
	ifname.startswith("-"):
	
	continue

print("%s=%r\n"%(name,value))
~~~
>	运行结果：

	__cached__='C:\\Users\\33916\\AppData\\Local\\Programs\\Python\\Python311\\Lib\\__pycache__\\string.cpython-311.pyc'
	
	__doc__='A collection of string constants.\n\nPublic module variables:\n\nwhitespace -- a string containing all ASCII whitespace\nascii_lowercase -- a string containing all ASCII lowercase letters\nascii_uppercase -- a string containing all ASCII uppercase letters\nascii_letters -- a string containing all ASCII letters\ndigits -- a string containing all ASCII decimal digits\nhexdigits -- a string containing all ASCII hexadecimal digits\noctdigits -- a string containing all ASCII octal digits\npunctuation -- a string containing all ASCII punctuation characters\nprintable -- a string containing all ASCII characters considered printable\n\n'
	
	__file__='C:\\Users\\33916\\AppData\\Local\\Programs\\Python\\Python311\\Lib\\string.py'
	
	__name__='string'
	
	__package__=''
	
	ascii_letters='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
	
	ascii_lowercase='abcdefghijklmnopqrstuvwxyz'
	
	ascii_uppercase='ABCDEFGHIJKLMNOPQRSTUVWXYZ'
	
	digits='0123456789'
	
	hexdigits='0123456789abcdefABCDEF'
	
	octdigits='01234567'
	
	printable='0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'
	
	punctuation='!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
	
	whitespace=' \t\n\r\x0b\x0c'

---

二、***textwarp模块：格式化文本段落***

1、**fill（）函数格式化文本输出**
例子:
~~~python
import textwrap

sample_text='''

MarilynMonroewasafamousAmericanmovieactressfromthe1950sandearly1960s.HerlifeisbeingdetailedinanewmovieonNetflix,Blonde.ItstarsAnadeArmasasMarilynMonroe.

Monroewaswell-knownforhercostumesinthemovies.SheworeabrightpinklongdresstosingthesongDiamondsAreaGirl'sBestFriend.Andmostfamously,sheworeawhitedressthatblewupasshewalkedoverthesubwayinthemovieTheSevenYearItch.

'''

s=textwrap.fill(sample_text,width=100)

print(s)
~~~
>	运行结果：

	 Marilyn Monroe was a famous American movie actress from the 1950s and early 1960s.Her life is being
	
	detailed in a new movie on Netflix, Blonde. It stars Ana de Armas as Marilyn Monroe. Monroe was
	
	well-known for her costumes in the movies. She wore a bright pink long dress to sing the song
	
	Diamonds Are a Girl's Best Friend. And most famously, she wore a white dress that blew up as she
	
	walked over the subway in the movie The Seven Year Itch.

使用fill（）函数实现了文本内容左对齐。其中width参数表示的是文本的输出宽度。

例如若width参数值为50，即s=textwrap.fill(sample_text,width=50)

>	输出结果：

	 Marilyn Monroe was a famous American movie
	
	actress from the 1950s and early 1960s.Her life is
	
	being detailed in a new movie on Netflix, Blonde.
	
	It stars Ana de Armas as Marilyn Monroe. Monroe
	
	was well-known for her costumes in the movies. She
	
	wore a bright pink long dress to sing the song
	
	Diamonds Are a Girl's Best Friend. And most
	
	famously, she wore a white dress that blew up as
	
	she walked over the subway in the movie The Seven
	
	Year Itch.

上面实现了左对齐，但是右面由于缩进或空格，并不是整齐的。因此——

---

2、**去除现有的缩进和空格**

通常使用*dedent()*函数来去除文本中的空白。

例子：
~~~python
import textwrap

sample_text='''

MarilynMonroewasafamousAmericanmovieactressfromthe1950sandearly1960s.HerlifeisbeingdetailedinanewmovieonNetflix,Blonde.ItstarsAnadeArmasasMarilynMonroe.

Monroewaswell-knownforhercostumesinthemovies.SheworeabrightpinklongdresstosingthesongDiamondsAreaGirl'sBestFriend.Andmostfamously,sheworeawhitedressthatblewupasshewalkedoverthesubwayinthemovieTheSevenYearItch.

'''

dedent_text=textwrap.dedent(sample_text).strip()             #删除空格

for width in[100,200]:

	print("{0}Columns:\n".format(width))
	
	print(textwrap.fill(dedent_text,width=width))
	
	print("#######################################")
~~~

>	运行结果：

	100 Columns（列）:
	
	Marilyn Monroe was a famous American movie actress from the 1950s and early 1960s.Her life is being
	
	detailed in a new movie on Netflix, Blonde. It stars Ana de Armas as Marilyn Monroe. Monroe was
	
	well-known for her costumes in the movies. She wore a bright pink long dress to sing the song
	
	Diamonds Are a Girl's Best Friend. And most famously, she wore a white dress that blew up as she
	
	walked over the subway in the movie The Seven Year Itch.
	
	#######################################
	
	200 Columns:
	
	Marilyn Monroe was a famous American movie actress from the 1950s and early 1960s.Her life is being detailed in a new movie on Netflix, Blonde. It stars Ana de Armas as Marilyn Monroe. Monroe was
	
	well-known for her costumes in the movies. She wore a bright pink long dress to sing the song Diamonds Are a Girl's Best Friend. And most famously, she wore a white dress that blew up as she walked
	
	over the subway in the movie The Seven Year Itch.
	
	#######################################

---

3、**缩进块**

与*dedent()*不同的是，*indent()*函数可以实现文本加上特定的前缀。用于默写特定的文本表达。

例子：
~~~python
import textwrap

sample_text='''

MarilynMonroewasafamousAmericanmovieactressfromthe1950sandearly1960s.HerlifeisbeingdetailedinanewmovieonNetflix,Blonde.ItstarsAnadeArmasasMarilynMonroe.

Monroewaswell-knownforhercostumesinthemovies.SheworeabrightpinklongdresstosingthesongDiamondsAreaGirl'sBestFriend.Andmostfamously,sheworeawhitedressthatblewupasshewalkedoverthesubwayinthemovieTheSevenYearItch.

'''

dedent_text=textwrap.dedent(sample_text).strip()

wrapperd=textwrap.fill(dedent_text,width=50)

wrapperd+="\n\nSecondparagraphafterablankline."

final=textwrap.indent(wrapperd,">")

print("Quotedblock:\n")

print(final)
~~~
>	运行结果：

	Quoted block:
	
		Marilyn Monroe was a famous American movie actress
		
		from the 1950s and early 1960s.Her life is being
		
		detailed in a new movie on Netflix, Blonde. It
		
		stars Ana de Armas as Marilyn Monroe. Monroe was
		
		well-known for her costumes in the movies. She
		
		wore a bright pink long dress to sing the song
		
		Diamonds Are a Girl's Best Friend. And most
		
		famously, she wore a white dress that blew up as
		
		she walked over the subway in the movie The Seven
	
		Year Itch.
		
		Second paragraph after a blank line.

---

为了控制具体那一行文本文字具有前缀，可以**使用callable对象作为indent（）的predicate参数。以此为各行文本调用此callable，并未返回值为True的行添加前缀。**

例子：
~~~python
import textwrap

sample_text='''

MarilynMonroewasafamousAmericanmovieactressfromthe1950sandearly1960s.HerlifeisbeingdetailedinanewmovieonNetflix,Blonde.ItstarsAnadeArmasasMarilynMonroe.

Monroewaswell-knownforhercostumesinthemovies.SheworeabrightpinklongdresstosingthesongDiamondsAreaGirl'sBestFriend.Andmostfamously,sheworeawhitedressthatblewupasshewalkedoverthesubwayinthemovieTheSevenYearItch.

'''

def should_indent(line):
	
	print("Indent{0}".format(line))
	
	returnlen(line.strip())%2==0
	
	dedent_text=textwrap.dedent(sample_text)
	
	wrapped=textwrap.fill(dedent_text,width=100)
	
	final=textwrap.indent(wrapped,"EVEN\n",predicate=should_indent)
	
	print("\nQuotedblock\n")

print(final)
~~~
>	运行结果：

	Indent  Marilyn Monroe was a famous American movie actress from the 1950s and early 1960s.Her life is being
	
	Indent detailed in a new movie on Netflix, Blonde. It stars Ana de Armas as Marilyn Monroe. Monroe was
	
	Indent well-known for her costumes in the movies. She wore a bright pink long dress to sing the song
	
	Indent Diamonds Are a Girl's Best Friend. And most famously, she wore a white dress that blew up as she
	
	Indent walked over the subway in the movie The Seven Year Itch.
	
	Quoted block
	
	 Marilyn Monroe was a famous American movie actress from the 1950s and early 1960s.Her life is being
	
	detailed in a new movie on Netflix, Blonde. It stars Ana de Armas as Marilyn Monroe. Monroe was
	
	well-known for her costumes in the movies. She wore a bright pink long dress to sing the song
	
	EVEN
	
	Diamonds Are a Girl's Best Friend. And most famously, she wore a white dress that blew up as she
	
	EVEN
	
	walked over the subway in the movie The Seven Year Itch.

---

4、**首行缩进**

使用*indent*函数可以实现首行缩进。

例子：
~~~python
import textwrap

sample_text='''

MarilynMonroewasafamousAmericanmovieactressfromthe1950sandearly1960s.HerlifeisbeingdetailedinanewmovieonNetflix,Blonde.ItstarsAnadeArmasasMarilynMonroe.

Monroewaswell-knownforhercostumesinthemovies.SheworeabrightpinklongdresstosingthesongDiamondsAreaGirl'sBestFriend.Andmostfamously,sheworeawhitedressthatblewupasshewalkedoverthesubwayinthemovieTheSevenYearItch.

'''

def should_indent(line):
	
	print("Indent{0}".format(line))
	returnlen(line.strip())%2==0
	
	dedent_text=textwrap.dedent(sample_text).strip()
	
			print(textwrap.fill(dedent_text,initial_indent="",subsequent_indent=""*4,width=50))
~~~
>	运行结果：

	 Marilyn Monroe was a famous American movie
	
	    actress from the 1950s and early 1960s.Her
	
	    life is being detailed in a new movie on
	
	    Netflix, Blonde. It stars Ana de Armas as
	
	    Marilyn Monroe. Monroe was well-known for her
	
	    costumes in the movies. She wore a bright pink
	
	    long dress to sing the song Diamonds Are a
	
	    Girl's Best Friend. And most famously, she
	
	    wore a white dress that blew up as she walked
	
	    over the subway in the movie The Seven Year
	
	    Itch.

---

三、***正则表达式***

正则表达式是一种形式化语法描述的文本处理模式。模式可以被理解成一组指令，然后执行这些指令并提供一个字符串作为输入，将生成一个匹配子集或者生成源字符串的一个修改版本。

1、**查找模式**

re模块最常见的用法是查找模式，**search()函数**可以实现文本的读取和扫描文本，在查找目标对象时，若查找到目标对象，就返回一个Match对象。如果没有找到目标对象，search()函数返回None。

每一个Match对象包含相关匹配实质的信息，包括原输入字符串、所使用的正则表达式以及模式在原字符串中出现的位置。

例子：
~~~python
import re

#定义基本的变量

text="iamafool,anythingidon'tknow!butpythonisaeasyandgoodcomputerlanguage!"

need_search=input("inputwhatyouwanttosearch:")

#引用search函数s表示字符查找的起始位置，e表示被查找字符串的结束位置

try:

	match=re.search(need_search,text)  #search函数的参数先是要查找的目标、再是被查找的文本。
	
	s=match.start()
	
	e=match.end()
	
		print("Found{0}intextfrom{1}to{2}['{3}']".format(match.re.pattern,s,e,text[s:e]))

except AttributeError as e:

	print("Don'tfindwhatyouwant！\n",e)
~~~
>	运行结果;

	input what you want to search :computer
	
	Found computer in text from 67 to 75 ['computer']

___

2、**编译表达式**
re库包括模块级函数，可以处理作为文本字符串的正则表达式，但对于程序频繁使用的表达式而言，编译他们更为高效。*compile（）函数*会把一个字符串转换成一个Regexobject。
例子：
~~~python
import re  
#Precompile the pattern  
regexes=[  
	re.compile(p)  
	for p in ["this","that"]  
]  
text="Does this match the patter?"  
  
print("Text:{0}\n".format(text))  
  
for regexe in regexes:  
	print("Seeking '{0}'-->".format(regexe.pattern),end=" ")  
	if regexe.search(text):  
	print("match!")  
	else:  
	print("no match!")
~~~
>	运行结果：
	
	Text:Does this match the patter?

	Seeking 'this'--> match!
	Seeking 'that'--> no match!
原理分析：这行代码的作用是将字符串列表 `["this", "that"]` 中的每个模式字符串进行编译，然后将编译后的正则表达式对象添加到 `regexes` 列表中。通过将模式字符串编译为正则表达式对象，我们可以在后续的代码中重复使用这些编译后的正则表达式对象，而不需要每次都重新编译模式字符串。

---

3、**多重匹配**
在之前的search()函数中仅能单一的查找字面量文本字符串的单个实例。而findall（）函数会返回输入中与模式匹配而不重叠的所有子串。
例子:
~~~ python
#导入re库
import re  
text="abbaaabbbbbbaaaaaaaaa"
#设置检索字
pattern="ab"
#设置迭代器
count=0
#遍历文本
for i in re.findall(pattern,text):  
	count+=1  
	print("Found '{0}'".format(i))  
print(count)
运行结果：
Found 'ab'
Found 'ab'
2
~~~
finditer()函数亦可以实现多呈匹配
但---finditer()返回一个迭代器会生成Match实例，而不像findall()那样返回字符串。
例子：
~~~python
import re  
text="abbaaabbbbbbaaaaaaaaa"  
pattern="ab"  
count=0  
	for i in re.finditer(pattern,text):  
	count+=1  
	s=i.start()  
	e=i.end()  
	print("Found '{0} at[{1}:{2}]'".format(i,s,e))  
print(count)
~~~
>		运行结果：
		Found '<re.Match object; span=(0, 2), match='ab'> at[0:2]'
		Found '<re.Match object; span=(5, 7), match='ab'> at[5:7]'
		2
很明显，返回的是一个迭代器。

---

4、模式语法
除了简单的字面量文本字符串，正则表达式还支持更为强大的模式，此模式可以重复，可以锚定到输入中不同的逻辑位置，可以用紧凑的形式表述而不需要再次模式中提供每一个字面量字符。可以结合字面量文本值和元字符来使用所有这些特性，元字符是re实现的正则表达式模式语法的一个部分。
例子：
~~~python
import re  
def text_patterns(text,patterns):  
	for pattern,desc in patterns:  
		print("'{0}' ({1})\n".format(pattern,desc))  
		print("'{0}'".format(text))  
		for match in re.finditer(pattern,text):  
			s=match.start()  
			e=match.end()  
			substr=text[s:e]  
			n_balckslashes=text[:s].count("\\")  
			prefix="."*(s+n_balckslashes)  
			print("{0} {1}".format(prefix,substr))  
		print()  
	return  
if __name__=="__main__":  
	text="abbaaaabbbbaaaaaaaaa"  
	patterns=[('ab',"'a' followed by 'b'"),]  
	text_patterns(text,patterns)
~~~

>	运行结果：
	
	'ab' ('a' followed by 'b')

	'abbaaaabbbbaaaaaaaaa'
	 ab
	...... ab
上面代码定义了一个函数，从而实现多重匹配功能的使用。
5、**重复**
在re模块中存在5种便是重复的方法。
若在函数后面有元字符*，则表示重复0次或多次。如果把*替换成+，则必须出现1次才能匹配。使用？表示出现次数0次或1次。如果要指定次数，这需要在模式后使用{m}。其中m是模式重复出现的次数。最后，如果要允许一个可变但有限的重复的次数，则可以使用{m,n}，这里m是最小数。n为最大数。
例子：
~~~python
import re  
def text_patterns(text,patterns):  
	for pattern,desc in patterns:  
		print("'{0}' ({1})\n".format(pattern,desc))  
		print("'{0}'".format(text))  
		for match in re.finditer(pattern,text):  
			s=match.start()  
			e=match.end()  
			substr=text[s:e]  
			n_balckslashes=text[:s].count("\\")  
			prefix="."*(s+n_balckslashes)  
			print("{0} {1}".format(prefix,substr))  
		print()  
	return  
if __name__=="__main__":  
	text="abbaabbba"  
	patterns=[('ab',"'a' followed by 'b'"),  
		('ab+','a followed by one or more b '),  
		('ab*',"'a' followed by zero or more 'b'"),  
		('ab?',"'a' followed by zero or one 'b'"),  
		('ab{3}',"'a' followed by three 'b'"),  
		('ab{2,3}',"'a' followed by two to three 'b'")]  
	text_patterns(text,patterns)
~~~
>运行结果：
				'ab' ('a' followed by 'b')

				'abbaabbba'
				 ab
				.... ab
				
				'ab+' (a followed by one or more b )
				
				'abbaabbba'
				 abb
				.... abbb
				
				'ab*' ('a' followed by zero or more 'b')
				
				'abbaabbba'
				 abb
				... a
				.... abbb
				........ a
				
				'ab?' ('a' followed by  zero or one 'b')
				
				'abbaabbba'
				 ab
				... a
				.... ab
				........ a
				
				'ab{3}' ('a' followed by three 'b')
				
				'abbaabbba'
				.... abbb
				
				'ab{2,3}' ('a' followed by two to three 'b')
				
				'abbaabbba'
				 abb
				 .... abbb
6、**字符集**
字符集是一组*字符*，包含可以与模式中当前位置匹配的所有字符，例如，[ab]可以匹配成a或b
#示例代码
~~~python
import re  
def text_patterns(text,patterns):  
	for pattern,desc in patterns:  
		print("'{0}' ({1})\n".format(pattern,desc))  
		print("'{0}'".format(text))  
		for match in re.finditer(pattern,text):  
			s=match.start()  
			e=match.end()  
			substr=text[s:e]  
			n_balckslashes=text[:s].count("\\")  
			prefix="."*(s+n_balckslashes)  
			print("{0} {1}".format(prefix,substr))  
		print()  
	return  
if __name__=="__main__":  
	text="abbaabbba"  
	patterns=[('[ab]','either a or b'),  
	('a+[ab]+','a followed one or more a or b'),  
	("a[ab]+?","a followed one or more a or b ,not gready")]  
	text_patterns(text,patterns)
~~~
> 运行结果：
	'[ab]' (either a or b)

	'abbaabbba'
	 a
	. b
	.. b
	... a
	.... a
	..... b
	...... b
	....... b
	........ a
	
	'a+[ab]+' (a followed one  or more a or b)
	
	'abbaabbba'
	 abbaabbba
	
	'a[ab]+?' (a followed one or more a or b ,not gready)
	
	'abbaabbba'
	 ab
	... aa
---
字符集还可以来排除特定的字符。尖字符（^）意味着要查找不在这个尖字符后面的集合中的字符。
#示例代码 
~~~python
import re  
	def text_patterns(text,patterns):  
		for pattern,desc in patterns:  
		print("'{0}' ({1})\n".format(pattern,desc))  
		print("'{0}'".format(text))  
		for match in re.finditer(pattern,text):  
			s=match.start()  
			e=match.end()  
			substr=text[s:e]  
			n_balckslashes=text[:s].count("\\")  
			prefix="."*(s+n_balckslashes)  
			print("{0} {1}".format(prefix,substr))  
		print()  
	return  
if __name__=="__main__":  
	text="This is some text -- with punctuation."  
	patterns=[('[^-. ]+','sequence without -,.,or space')]  
	text_patterns(text,patterns)
~~~
> 运行结果：
	'[^-. ]+' (sequence without -,.,or space)
	'This is some text -- with punctuation.'
	 This
	..... is
	........ some
	............. text
	..................... with
	.......................... punctuation
此代码实现了排除-号和.号。
随着字符集的变大，键入的每一个应当（或不应当）匹配的字符串会变得很麻烦。可以使用一个更简洁的格式，利用字符区间来定义一个字符集，包含指定的起点和终点之间的所有连续的字符集
#示例代码 
~~~python
import re  
def text_patterns(text,patterns):  
	for pattern,desc in patterns:  
		print("'{0}' ({1})\n".format(pattern,desc))  
		print("'{0}'".format(text))  
			for match in re.finditer(pattern,text):  
				s=match.start()  
				e=match.end()  
				substr=text[s:e]  
				n_balckslashes=text[:s].count("\\")  
				prefix="."*(s+n_balckslashes)  
				print("{0} {1}".format(prefix,substr))  
		print()  
	return  
if __name__=="__main__":  
	text="This is some text -- with punctuation."  
	patterns=[('[a-z]+','sequence of lowercase letters'),  
				('[A-Z]+','squence of uppercase letters'),  
				('[a-zA-z]+','sequence of lower- or uppercase letters'),  
				('[A-Z][a-z]+','one uppercase followed by lowercase')]  
	text_patterns(text,patterns)
~~~
> 运行结果：
	'[a-z]+' (sequence of lowercase letters)

	'This is some text -- with punctuation.'
	. his
	..... is
	........ some
	............. text
	..................... with
	.......................... punctuation
	
	'[A-Z]+' (squence of uppercase letters)
	
	'This is some text -- with punctuation.'
	 T
	
	'[a-zA-z]+' (sequence of lower- or uppercase letters)
	
	'This is some text -- with punctuation.'
	 This
	..... is
	........ some
	............. text
	..................... with
	.......................... punctuation
	
	'[A-Z][a-z]+' (one uppercase followed by lowercase)
	
	'This is some text -- with punctuation.'
	 This
<span style="color:red">休息一下，看看抖音吧</span>
[抖音-记录美好生活 (douyin.com)](https://www.douyin.com/)
