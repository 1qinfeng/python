# 第一题蛇形填数

## 题目

如下图所示，小明用从 11 开始的正整数“蛇形”填充无限大的矩阵。
1 2 6 7 15 ... 
3 5 8 14 ... 
4 9 13 ... 
10 12 ... 
11 ... 
...
容易看出矩阵第二行第二列中的数是 55。请你计算矩阵中第 20 行第 20列的数是多少？

## 解题：

观察数组，找规律。易得$1=(1-1)*4+1$,$5=(2-1)*4+1$,$13=(3-1)*4+5$,则第n行满足$(n-1)*4+(n-2)*4+.....+1$
则采用遍历1--20,$(i-1)*4+1$的和即可。

## 代码


~~~python
num=1
for i in range(1,21):
	num+=(i-1)*4
print(num)
~~~
---
# 第二题物品摆放

## 题目

小蓝有一个超大的仓库，可以摆放很多货物。
现在，小蓝有 n 箱货物要摆放在仓库，每箱货物都是规则的正方体。小蓝规定了长、宽、高三个互相垂直的方向，每箱货物的边都必须严格平行于长、宽、高。小蓝希望所有的货物最终摆成一个大的长方体。即在长、宽、高的方向上分别堆 L、W、H 的货物,满足 n=L×W×H。
给定 n，请问有多少种堆放货物的方案满足要求。
例如，当 n=4 时，有以下 66 种方案：1×1×4、1×2×2、1×4×1、2×1×2、2×2×1、4×1×11×1×4、1×2×2、1×4×1、2×1×2、2×2×1、4×1×1。
请问，当 n=2021041820210418 （注意有 16 位数字）时，总共有多少种方案？
提示：建议使用计算机编程解决问题。

## 解题

找出n的因子

很容易地想到三次遍历1-2021041820210418，若出现三个整数i,j,k相乘为n时输出i,j,k。但由于遍历的范围较大，需要消耗大量的内存和有运行时间，并不是很现实。另一种方法是找出n的因子，在遍历其因子i，j，k，使得j*I*K=n,输出j,i,k。

## 代码

~~~python
n=2021041820210418  
count=0  
factors = []  
#找出n的因子，n的因子不会大于n**0.5,所以只需遍历到n**0.5
for i in range(1,int(n**0.5)+1):  
	if n%i==0:  
		factors.append(i)  
		if i!=n//i:  
			factors.append(n//i)  
factors.sort()  
for j in factors:  
	for k in factors:  
		for x in factors:  
			if x*j*k==n:  
				count+=1  
print(count)
~~~
---
# 第三题 著名的杨辉三角形

## 题目

下面是著名的杨辉三角形：
![image-20230526002859919](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230526002859919.png)
如果我们按从上到下、从左到右的顺序把所有数排成一列，可以得到如下数列： 1,1,1,1,2,1,1,3,3,1,1,4,6,4,1,⋯1,1,1,1,2,1,1,3,3,1,1,4,6,4,1,⋯
给定一个正整数 N，请你输出数列中第一次出现 N 是在第几个数？

## 解题：



## 代码




---
# **第四道题进制转换**

## 题目

九进制正整数 ​2022 转换成十进制等于多少？

## 解题
方法一：利用进制的原理来进行解题。
方法二：利用int（）函数来实现

## 代码


~~~python
#方法一：进制的定义
print(2*9**3+0*9**2+2*9**1+2*9**0)
#方法二：int()函数
print(int('2022',9))
~~~
##  知识点

int()函数用法

| 用法                                 | 例子                           |
| ------------------------------------ | ------------------------------ |
| 将字符转换成整形                     | int(1.2)=1                     |
| 进制的转换（将其他进制转换成十进制） | print(int(‘n’,’要转换的进制’)) |



# 第五题 等差素数数列

## 题目

2,3,5,7,11,13,.... 是素数序列。 类似：7,37,67,97,127,15 这样完全由素数组成的等差数列，叫等差素数数列。
上边的数列公差为 30，长度为 66。
2004年，格林与华人陶哲轩合作证明了：存在任意长度的素数等差数列。 这是数论领域一项惊人的成果！有这一理论为基础，请你借助手中的计算机，满怀信心地搜索：
长度为 10 的等差素数列，其公差最小值是多少？

解题思路:
1.  定义一个函数`is_prime(n)`来判断一个数`n`是否为素数。可以使用试除法或者更高效的素数测试算法来实现该函数。    
2.  定义一个函数`find_prime_arithmetic_sequence(length)`来搜索长度为`length`的等差素数列的最小公差。该函数将返回最小公差值。    
3.  在`find_prime_arithmetic_sequence(length)`函数中，初始化一个空列表`primes`来存储找到的素数。   
4.  使用一个循环来生成素数，直到找到足够数量的素数为止。可以从2开始逐个增加数值，并使用`is_prime()`函数来判断每个数是否为素数。将素数添加到`primes`列表中。    
5.  初始化一个变量`smallest_difference`来存储最小公差的初始值，可以设置为一个较大的数。    
6.  使用另一个循环来遍历`primes`列表，从第二个素数开始。计算当前素数与前一个素数的差，将差值存储在变量`difference`中。   
7.  检查`difference`是否小于`smallest_difference`，如果是，则更新`smallest_difference`为`difference`的值。   
8.  继续遍历`primes`列表，直到找到长度为`length`的等差素数列为止。   
9.  返回`smallest_difference`作为最小公差值。   
10.  在主程序中，调用`find_prime_arithmetic_sequence(length)`函数，
## 代码
~~~python
def panduan(a):  
	for i in range(2,a):  
		if a%i == 0:  
			return False  
	return True  
def shushu():  
	a=0  
	b=0  
	for i in range(2,1000):  
		if not panduan(i):  
			continue  
		else:  
		for j in range(1,500):  
			b=i  
			for k in range(10):  
				b=b+j  
				if not panduan(b):  
					break  
				else:  
					a=a+1  
			if a==9:  
				return j  
			else:  
				a=0  
print(shushu())
~~~
---
# [NOIP2002 普及组] 级数求和

## 题目描述

已知：$S_n= 1+\frac{1}{2}+\frac{1}{3}+…+\frac{1}{n}$。显然对于任意一个整数 $k$，当 $n$ 足够大的时候，$S_n>k$。

现给出一个整数 $k$，要求计算出一个最小的 $n$，使得 $S_n>k$。

## 输入格式

一个正整数 $k$。

## 输出格式

一个正整数 $n$。

## 样例 #1

### 样例输入 #1

```
1
```

### 样例输出 #1

```text
2
```

## 提示

**【数据范围】**

对于 $100\%$ 的数据，$1\le k \le 15$。
> 解题
方法一：直接循环求解（对较小的k有效）
~~~python
def calculate_n(k):  
	n = 1  
	Sn = 0  
	while Sn <= k:  
		Sn += 1 / n  
		n += 1  
		return n - 1 # 修正：返回 n-1，因为在退出循环时，Sn 已经大于 k  
k =int(input())  
result = calculate_n(k)  
print(result)
~~~
方法二：欧拉常数，近似求解
当k较大时，可以采用数学方法来快速估计n的值，而不需要进行逐个迭代计算。
根据已知的级数公式，Sₙ = 1 + 1/2 + 1/3 + ... + 1/𝑛，该级数被称为调和级数。我们知道，调和级数是发散的，也就是说Sn会趋向于无穷大。
然而，我们可以使用自然对数的性质来近似估计Sn的值。根据欧拉常数（Euler's constant）𝑒 ≈ 2.71828，我们有以下近似公式：
Sₙ ≈ 𝑛 + ln(𝑛) + γ
其中，𝛾是欧拉常数的近似值，约为0.57721。根据这个近似公式，我们可以估计出一个较小的n，使得Sn > k。
下面是一个使用近似估计算法的Python代码示例：
~~~python
import math

def calculate_n_approximation(k):
    n = int(math.exp(k - 0.57721))  # 使用近似公式计算n的估计值
    while calculate_Sn(n) <= k:
        n += 1
    return n

def calculate_Sn(n):
    Sn = 0
    for i in range(1, n + 1):
        Sn += 1 / i
    return Sn

k=int(input())
result = calculate_n_approximation(k)
print("通过近似估计算法得到的最小n使得Sn > k是：", result)
~~~
通过运行以上代码，您可以输入一个较大的整数k，并使用近似估计算法快速计算出满足Sn > k的最小n。请注意，近似估计算法是一种近似方法，因此结果可能不是精确的，但可以在较短时间内得到一个接近的估计值。其中==math.exp()==表示e次幂
---
# [NOIP2005 普及组] 陶陶摘苹果

## 题目描述

陶陶家的院子里有一棵苹果树，每到秋天树上就会结出 $10$ 个苹果。苹果成熟的时候，陶陶就会跑去摘苹果。陶陶有个 $30$ 厘米高的板凳，当她不能直接用手摘到苹果的时候，就会踩到板凳上再试试。


现在已知 $10$ 个苹果到地面的高度，以及陶陶把手伸直的时候能够达到的最大高度，请帮陶陶算一下她能够摘到的苹果的数目。假设她碰到苹果，苹果就会掉下来。

## 输入格式

输入包括两行数据。第一行包含 $10$ 个 $100$ 到 $200$ 之间（包括 $100$ 和 $200$ ）的整数（以厘米为单位）分别表示 $10$ 个苹果到地面的高度，两个相邻的整数之间用一个空格隔开。第二行只包括一个 $100$ 到 $120$ 之间（包含 $100$ 和 $120$ ）的整数（以厘米为单位），表示陶陶把手伸直的时候能够达到的最大高度。

## 输出格式

输出包括一行，这一行只包含一个整数，表示陶陶能够摘到的苹果的数目。

## 样例 #1
### 样例输入 #1
```
100 200 150 140 129 134 167 198 200 111
110
```
### 样例输出 #1
```
5
```
>解题：只需陶陶所能达到的最大高度大与苹果的高度即可栽倒苹果
~~~python
apple_height=input().split(' ')  
human_height=int(eval(input()))  
def get_apple():  
	count=0  
	for i in apple_height:  
		if human_height+30 >=int(i):  
		count+=1  
	return count  
a=get_apple()  
print(a)
~~~
---
# [NOIP2005 普及组] 校门外的树
## 题目描述
某校大门外长度为 $l$ 的马路上有一排树，每两棵相邻的树之间的间隔都是 $1$ 米。我们可以把马路看成一个数轴，马路的一端在数轴 $0$ 的位置，另一端在 $l$ 的位置；数轴上的每个整数点，即 $0,1,2,\dots,l$，都种有一棵树。
由于马路上有一些区域要用来建地铁。这些区域用它们在数轴上的起始点和终止点表示。已知任一区域的起始点和终止点的坐标都是整数，区域之间可能有重合的部分。现在要把这些区域中的树（包括区域端点处的两棵树）移走。你的任务是计算将这些树都移走后，马路上还有多少棵树。
## 输入格式
第一行有两个整数，分别表示马路的长度 $l$ 和区域的数目 $m$。
接下来 $m$ 行，每行两个整数 $u, v$，表示一个区域的起始点和终止点的坐标。
## 输出格式
输出一行一个整数，表示将这些树都移走后，马路上剩余的树木数量。
## 样例 #1
### 样例输入 #1
```
500 3
150 300
100 200
470 471
```
### 样例输出 #1
```
298
```
## 提示
**【数据范围】**
- 对于 $20\%$ 的数据，保证区域之间没有重合的部分。
- 对于 $100\%$ 的数据，保证 $1 \leq l \leq 10^4$，$1 \leq m \leq 100$，$0 \leq u \leq v \leq l$。

**【题目来源】**

NOIP 2005 普及组第二题
>解题：
<center>常规解法：

首先，将输入的马路长度和区域数量储存在一个列表中，然后遍历马路长度，将元素要加到list1中，再遍历区域数量，输入值，在遍历值的区域数，将元素储存在list2中，然后去除重复元素，遍历list2的元素，如果遍历的元素在list1中，则移除该元素。后输出list1的长度，即为剩下的树的数量。
~~~python
a=input().split(" ")  
tree_num=int(a[0])  
area_numb=int(a[1])  
list1=[]  
list2=[]  
for i in range(1,tree_num+1):  
	list1.append(i)  
for j in range(area_numb):  
	s=input().split()  
	for k in range(int(s[0]),int(s[1])+1):  
		list2.append(k)  
list2=list(set(list2))  
for b in list2:  
	if b in list1:  
		list1.remove(b)  
print(len(list1)+1)
~~~
<center>简便算法:

这段代码的作用是计算在给定的马路上，移走一些区域内的树木后，剩余的树木数量。
首先，通过 `input().split()` 获取输入的马路长度 `l` 和区域数量 `m`。
然后，创建一个长度为 `l+1` 的列表 `trees`，用于表示马路上每个位置的树木状态。初始时，所有位置都有树木，所以列表中的元素都为 1。
接下来，通过循环 `m` 次，获取每个区域的起始点和终止点，并将这些区域内的树木设置为 0，表示移走了树木。
最后，通过求和计算列表 `trees` 中值为 1 的元素的数量，即为剩余的树木数量，将结果输出。
这段代码的时间复杂度为 O(l + m)，其中 l 是马路的长度，m 是区域的数量。
<span style='color:green'><center>代码如下：</span>
~~~python
l, m = map(int, input().split())
trees = [1] * (l + 1)
for _ in range(m):
    start, end = map(int, input().split())
    for i in range(start, end + 1):
        trees[i] = 0
remaining_trees = sum(trees)
print(remaining_trees)
~~~
>注意：

| 名称 | 用法 | |
| ---- | ---- |----|
| map()     |map(数据类型，被转换的数据)      |可以将数据转换成指定的数据类型|
---
# [NOIP2006 普及组] 明明的随机数

## 题目描述

明明想在学校中请一些同学一起做一项问卷调查，为了实验的客观性，他先用计算机生成了 $N$ 个 $1$ 到 $1000$ 之间的随机整数 $(N\leq100)$，对于其中重复的数字，只保留一个，把其余相同的数去掉，不同的数对应着不同的学生的学号。然后再把这些数从小到大排序，按照排好的顺序去找同学做调查。请你协助明明完成“去重”与“排序”的工作。

## 输入格式

输入有两行，第 $1$ 行为 $1$ 个正整数，表示所生成的随机数的个数 $N$。

第 $2$ 行有 $N$ 个用空格隔开的正整数，为所产生的随机数。

## 输出格式

输出也是两行，第 $1$ 行为 $1$ 个正整数 $M$，表示不相同的随机数的个数。

第 $2$ 行为 $M$ 个用空格隔开的正整数，为从小到大排好序的不相同的随机数。

## 样例 #1

### 样例输入 #1

```
10
20 40 32 67 40 20 89 300 400 15
```

### 样例输出 #1

```
8
15 20 32 40 67 89 300 400
```

## 提示

NOIP 2006 普及组 第一题
解题方法：
关键在于如何去除重复的元素，如何输出目标格式——字符串形式、从小到大排列
### <center> 代码如下

~~~python
N = int(input())  
numbers = list(map(int, input().split()))  
  
# 去重并排序  
unique_numbers = sorted(set(numbers))  
  
M = len(unique_numbers)  
print(M)  
  
# 输出不相同的随机数  
output = " ".join(map(str, unique_numbers))  
print(output)
~~~
##  方法

| 目标                                                       | 实现的方法                       |
| ---------------------------------------------------------- | -------------------------------- |
| 去除重复元素                                               | 利用集合的特性）——不包含重复元素 |
| 输出字符串                                                 | jion()函数来接字符串             |
| 从小到大排列                                               | sorted()函数实现                 |
| 从大到小排列                                               | sorted(数据,reverse=True)实现    |
| 注意：使用join（）函数来拼接字符串时要确保数据类型为字符串 |                                  |
---
# [NOIP2012 普及组] 质因数分解

## 题目描述

已知正整数 $n$ 是两个不同的质数的乘积，试求出两者中较大的那个质数。

## 输入格式

输入一个正整数 $n$。

## 输出格式

输出一个正整数 $p$，即较大的那个质数。

## 样例 #1

### 样例输入 #1

```
21
```

### 样例输出 #1

```
7
```

## 提示

$1 \le n\le 2\times 10^9$

NOIP 2012 普及组 第一题

### 解题方法

常规解法：
1. 找出目标数字的所有因子（关键）
2. 两次遍历因子数集
3. 乘积为目标数字，返回因子数，并储存在列表中
4. 获取最大数（利用==max()函数==）

#### 代码

~~~python
n=int(input())  
list1=[]  
list2=[]  
for i in range(1,int(n**0.5)+1):  
	if n%i==0:  
		list1.append(i)  
		#难以理解，举一个例子：如果 n 除以 i 的结果不等于 i，说明还存在另一个因数，将 n 除以 i 的结果添加到 list1 列表中。（例如，如果 n=16，i=2，那么 16 除以 2 的结果是 8，需要将 8 作为另一个因数添加到列表中）  
		if n//i!=i:  
			list1.append(n//i)  
list1.sort()  
  
for j in list1:  
	for k in list1:  
		if j==1 or k==1:  
			pass  
		elif k*j==n:  
			lis1=[k,j]  
			list2.append(lis1)  
print(max(list2[0]))
~~~
高级解法：目前暂时未发现 

---
# [NOIP2004 普及组] 不高兴的津津

## 题目描述

津津上初中了。妈妈认为津津应该更加用功学习，所以津津除了上学之外，还要参加妈妈为她报名的各科复习班。另外每周妈妈还会送她去学习朗诵、舞蹈和钢琴。但是津津如果一天上课超过八个小时就会不高兴，而且上得越久就会越不高兴。假设津津不会因为其它事不高兴，并且她的不高兴不会持续到第二天。请你帮忙检查一下津津下周的日程安排，看看下周她会不会不高兴；如果会的话，哪天最不高兴。

## 输入格式

输入包括 $7$ 行数据，分别表示周一到周日的日程安排。每行包括两个小于 $10$ 的非负整数，用空格隔开，分别表示津津在学校上课的时间和妈妈安排她上课的时间。

## 输出格式

一个数字。如果不会不高兴则输出 $0$，如果会则输出最不高兴的是周几（用 $1, 2, 3, 4, 5, 6, 7$ 分别表示周一，周二，周三，周四，周五，周六，周日）。如果有两天或两天以上不高兴的程度相当，则输出时间最靠前的一天。

## 样例 #1

### 样例输入 #1

```
5 3
6 2
7 2
5 3
5 4
0 4
0 6
```

### 样例输出 #1

```
3
```

## 提示

NOIP2004 普及组第 1 题

- 2021-10-27：增加一组 hack 数据
- 2022-06-05：又增加一组 hack 数据
###解题思路
常规解法：
1. 计算每天的学习时间
2. 利用if-elif-else语句进行条件判断
3. 按照要求输出答案
#### 代码
~~~python
list1=[]  
for i in range(7):  
	study_time=map(int,input().split(" "))  
	list1.append(study_time)  
one=sum(list1[0])  
two=sum(list1[1])  
three=sum(list1[2])  
four=sum(list1[3])  
five=sum(list1[4])  
six=sum(list1[5])  
seven=sum(list1[6])  
#暴力判断
if one<8 and two<8 and three <8 and four <8 and five <8 and six <8 and seven<8:  
	print("0")  
elif one>=two and one>=three and one>=four and one>=five and one>=six and one>=seven:  
	print("1")  
elif two>=three and two>=four and two>=five and two >=six and two>=seven:  
	print("2")  
elif three>=four and three>=five and three >=six and three >=seven:  
	print("3")  
elif four>=five and four >=six and four>=seven:  
	print("4")  
elif five>=six and five>=seven:  
	print("5")  
elif six >=seven:  
	print("6")  
else:  
	print("7")
~~~
简便解法：
1. 计算每天的学习时间
2. 把所得每天的时间加入列表中，以便获取最大值
3. 返回最大值的索引
4. 最大值的索引+1即为星期数
5. 判断最大值是否满足条件
6. 输出正确值
#### 代码
~~~python
list=[]  
for i in range(7):  
	school_time,home_time=map(int,input().split(" "))  
	totol_time=school_time+home_time  
	list.append(totol_time)  
max_time=max(list)  
max_day=list.index(max_time)+1  
if max_time > 8:  
	print(max_day)  
else:  
	print(0)
~~~
##  知识点


| 知识点             | 内容                      |
| ------------------ | ------------------------- |
| 根据列表值返回索引 | 使用==index（values）函数 |
---
来一张照片养养眼！😍😍😍
![image-20230526003707527](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230526003707527.png)
---
# [NOIP2004 提高组] 津津的储蓄计划

## 题目描述

津津的零花钱一直都是自己管理。每个月的月初妈妈给津津 $300$ 元钱，津津会预算这个月的花销，并且总能做到实际花销和预算的相同。

为了让津津学习如何储蓄，妈妈提出，津津可以随时把整百的钱存在她那里，到了年末她会加上 $20\%$ 还给津津。因此津津制定了一个储蓄计划：每个月的月初，在得到妈妈给的零花钱后，如果她预计到这个月的月末手中还会有多于 $100$ 元或恰好 $100$ 元，她就会把整百的钱存在妈妈那里，剩余的钱留在自己手中。


例如 $11$月初津津手中还有 $83$ 元，妈妈给了津津 $300$ 元。津津预计$11$月的花销是 $180$ 元，那么她就会在妈妈那里存 $200$ 元，自己留下 $183$ 元。到了 $11$ 月月末，津津手中会剩下 $3$ 元钱。


津津发现这个储蓄计划的主要风险是，存在妈妈那里的钱在年末之前不能取出。有可能在某个月的月初，津津手中的钱加上这个月妈妈给的钱，不够这个月的原定预算。如果出现这种情况，津津将不得不在这个月省吃俭用，压缩预算。


现在请你根据 $2004$ 年 $1$ 月到 $12$ 月每个月津津的预算，判断会不会出现这种情况。如果不会，计算到 $2004$ 年年末，妈妈将津津平常存的钱加上 $20\%$ 还给津津之后，津津手中会有多少钱。

## 输入格式

$12$ 行数据，每行包含一个小于 $350$ 的非负整数，分别表示 $1$ 月到 $12$ 月津津的预算。

## 输出格式

一个整数。如果储蓄计划实施过程中出现某个月钱不够用的情况，输出 $-X$，$X$ 表示出现这种情况的第一个月；否则输出到 $2004$ 年年末津津手中会有多少钱。

注意，洛谷不需要进行文件输入输出，而是标准输入输出。

## 样例 #1

### 样例输入 #1

```
290
230
280
200
300
170
340
50 
90 
80 
200
60
```

### 样例输出 #1

```
-7
```

## 样例 #2

### 样例输入 #2

```
290 
230 
280 
200 
300 
170 
330 
50 
90 
80 
200 
60
```

### 样例输出 #2

```
1580
```
### <center>解题思路
这是一道逻辑题。看完答案后自然理解。
#### <center>代码
~~~python
given_money=0  
save_money=0  
month=0  
have_money=1  
mum_money=0  
for i in range(1,13):  
	given_money+=300  
	cost_money=int(input())  
	save_money=given_money-cost_money  
	if save_money <0:  
		have_money=0  
		month=i  
		break  
	mum_money+=int(save_money//100)  
	given_money=save_money%100  
if have_money !=0:  
	print(int(100*1.2*mum_money+given_money))  
else:  
month=month*-1  
	print(month)
~~~
---
# 车厢重组
## 题目描述
在一个旧式的火车站旁边有一座桥，其桥面可以绕河中心的桥墩水平旋转。一个车站的职工发现桥的长度最多能容纳两节车厢，如果将桥旋转 $180$ 度，则可以把相邻两节车厢的位置交换，用这种方法可以重新排列车厢的顺序。于是他就负责用这座桥将进站的车厢按车厢号从小到大排列。他退休后，火车站决定将这一工作自动化，其中一项重要的工作是编一个程序，输入初始的车厢顺序，计算最少用多少步就能将车厢排序。

## 输入格式

共两行。  

第一行是车厢总数 $N( \le 10000)$。

第二行是 $N$ 个不同的数表示初始的车厢顺序。

## 输出格式

一个整数，最少的旋转次数。

## 样例 #1

### 样例输入 #1

```
4
4 3 2 1
```

### 样例输出 #1

```
6
```

### 解题
这是一个冒泡排序法，相当于交换顺序
#### 代码
~~~python
num=int(input())  
count=0  
list=input().split(" ")  
n=0  
while n<num:  
	for j in range(1, num):  
	#交换位置
		index2 = j  
		index1 = j - 1  
		temp = list[index1]  
		if list[index2] < list[index1]:  
		list[index1] = list[index2]  
		list[index2] = temp  
	count += 1  
	n+=1  
print(count）
~~~

# 分糖果

## 题目描述

某个幼儿园里，有 $5$ 位小朋友编号依次为 $1,2,3,4,5$ 他们按照自己的编号顺序围坐在一张圆桌旁。他们身上有若干糖果，现在他们玩一个分糖果游戏。从 $1$ 号小朋友开始，将自己的糖果均分成 $3$ 份（如果有多余的糖果，就自己立即吃掉），自己留一份，其余两份分给和他相邻的两个小朋友。接着 $2,3,4,5$ 号小朋友也这样做。问一轮结束后，每个小朋友手上分别有多少糖果。

## 输入格式

一行，$5$ 个用空格隔开的 `int` 范围内的正整数，分别是游戏开始时  $1,2,3,4,5$ 号小朋友手里糖果的数量。

## 输出格式

$2$ 行，第 $1$ 行是用一个空格隔开的 $5$ 个整数，表示一轮游戏结束后  $1,2,3,4,5$ 号小朋友手里糖果的数量。第 $2$ 行是一个整数，表示一轮游戏过程中吃掉的糖果的总数。

## 样例 #1

### 样例输入 #1

```
8 9 10 11 12
```

### 样例输出 #1

```
11 7 9 11 6
6
```

## 题解：

1. 暴力解法：

```python
a,b,c,d,e = map(int, input().split(' '))
sum_all = a+b+c+d+e
a=a//3
b+=a
e+=a
b=b//3
c+=b
a+=b
c=c//3
b+=c
d+=c
d=d//3
c+=d
e+=d
e=e//3
d+=e
a+=e
print(a,b,c,d,e)
print(sum_all-(a+b+c+d+e))
```

2、巧妙解法：

