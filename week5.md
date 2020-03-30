# 程序设计思维与实践 第五周            &nbsp;&nbsp;&nbsp;    [返回首页](./index.md)&nbsp;&nbsp;  [上篇 CSP-201512-3](./CSP-201512-3.md)
## Problem A - 最大矩形
###  Description
给一个直方图，求直方图中的最大矩形的面积。例如，下面这个图片中直方图的高度从左到右分别是2, 1, 4, 5, 1, 3, 3, 他们的宽都是1，其中最大的矩形是阴影部分。
![ ](https://img-blog.csdnimg.cn/20200324113034190.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYzMzE1Mw==,size_16,color_FFFFFF,t_70)
### Input
输入包含多组数据。每组数据用一个整数n来表示直方图中小矩形的个数，你可以假定1 <= n <= 100000. 然后接下来n个整数h1, ..., hn, 满足 0 <= hi <= 1000000000. 这些数字表示直方图中从左到右每个小矩形的高度，每个小矩形的宽度为1。 测试数据以0结尾。

###  Output
对于每组测试数据输出一行一个整数表示答案。
### Sample Input
```cpp
7 2 1 4 5 1 3 3
4 1000 1000 1000 1000
0
```
###  Sample Output
```cpp
8
4000
```
### Idea
矩形面积=长度*高度。
当高度确定时，需要确定长度，也即左右边界：
``左边第一个小于该元素的位置``|``左边界``|``右边界``|``右边第一个小于该元素的位置``
找左右边界 <==> 找左右第一个小于该元素的位置，
右边界    -  左边界  + 1   = 矩形的长度
+ 右边界+1 = 右边第一个小于该元素的位置
+ 左边界     =  左边第一个小于该元素的位置 +1
 
两次遍历所有元素，利用单调递减栈分别往左，往右找到第一个比该元素小的位置。用两个数组保存左右边界信息。
+ 从左往右遍历，单调递减入栈可以找到左边第一个小于该元素的位置，
注意：每次保存左边界时，为[栈顶位置]+1,(栈空时为0)
+ 从右往左遍历，单调递减入栈可以找到右边第一个小于该元素的位置，
+注意： 每次保存右边界时，为[栈顶位置],(栈空时为N)
这样就可以保证 ``右``- ``左 `` = ``长度``
###  Codes
```cpp
#include<cstdio>  
using namespace std; 
const int MAX=100010;
long long A[MAX],L[MAX],R[MAX],S[MAX];
int N,size;
void getArea(int n){ 
	size=0;
	for(int i=0;i<n;i++){
	  scanf("%lld",&A[i]); 
	  while(size>0 and A[S[size-1]]>=A[i]) size--; //出栈 
	  L[i]=(size>0)?(S[size-1]+1):0;
	  S[size++]=i;	//压栈 
	} 
	size=0;
	for(int i=n-1;i>-1;i--){
	  while(size>0 and A[S[size-1]]>=A[i]) size--; //出栈 
	  R[i]=(size>0)?S[size-1]:n;
	  S[size++]=i;	//压栈 
	}
	long long cnt,T=-1;
	for(int i=0;i<n;i++){ 
		cnt=A[i]*(R[i]-L[i]);
		if(cnt>T) T=cnt;
	}
	printf("%lld\n",T);
}
int main(){
	while(~scanf("%d",&N)&&N){ 
		getArea(N);
	}
	return 0;
} 
```
## Problem B- TT's Magic Cat
###  Description
  Thanks to everyone's help last week, TT finally got a cute cat. But what TT didn't expect is that this is a magic cat.
  One day, the magic cat decided to investigate TT's ability by giving a problem to him. That is select n cities from the world map, and $a_[i]$ represents the asset value owned by the i-th city.
  Then the magic cat will perform several operations. Each turn is to choose the city in the interval $[l,r]$ and increase their asset value by $c$. And finally, it is required to give the asset value of each city after q operations.

Could you help TT find the answer?
###  Input
The first line contains two integers  $n,q (1≤n,q≤2⋅10^5)$  — the number of cities and operations.
The second line contains elements of the sequence a: integer numbers $a_1,a_2,...,a_n (−10^6≤a_{i}≤10^6)$ .
Then q lines follow, each line represents an operation. The i-th line contains three integers $l, r , c (1≤l≤r≤n,−10^5≤c≤10^5)$ for the $i$-th operation.
###  Output
Print $n$ integers $a_1,a_2,…,a_n$ one per line, and $a_i$ should be equal to the final asset value of the $i$-th city.
### Examples
####  Input
```cpp
4 2
-3 6 8 4
4 4 -2
3 3 1
```
#### Output
```cpp
-3 6 9 2
```
####  Input
```cpp
2 1
5 -2
1 2 4
```
#### Output
```cpp
9 2
```
####  Input
```cpp
1 2
0
1 1 -8
1 1 -6
```
#### Output
```cpp
 -14
```

### Idea
简单翻译：  魔术猫从世界地图中选择$n$个城市，而$a_[i]$代表第i个城市拥有的资产价值。然后，魔术猫将执行$q$个操作。 每次在区间$[l，r]$中选择城市，并将其资产价值都增加$c$。 最后，要求给出$q$次运算后每个城市的资产价值。
分析：问题要求解决的是对给定数组A，如何快速的对某个区间[l,r]同时增加常数c。这里可以选择用差分保存数组信息。即用数组B记录每个元素A[i]与上一个元素A[i-1]的差值，数组B的首元素B[0]记录为原数组的首元素A[0]即可。这样对区间``[l,r]``同时增加``c``也就是对``B[l]、B[r+1]``操作:``B[l]+c,B[r+1]-c``。
###  Codes
```cpp
#include<iostream> 
#include<cstdio> 
using namespace std;  
int main(){
    long long n,q,l,r,c;
    scanf("%lld %lld",&n,&q);
    long long A[n],B[n],i;
	for(i=0;i<n;i++)  
	{
		scanf("%lld",&A[i]);
		if(i==0) B[0]=A[0];
		else B[i]=A[i]-A[i-1];
	}	
	for(i=0;i<q;i++){
		scanf("%lld %lld %lld",&l,&r,&c);
		B[l-1] += c; B[r] -= c;
	}
	for(i=0;i<n;i++){
		if(i==0){
			A[0]=B[0];printf("%lld",A[0]);
		} 
		else {
			A[i]=A[i-1]+B[i];
			printf(" %lld",A[i]);
		} 
	}
	return 0;
} 
```
## Problem C- 平衡字符串
###  Description
一个长度为 n 的字符串 s，其中仅包含 'Q', 'W', 'E', 'R' 四种字符。
如果四种字符在字符串中出现次数均为 n/4，则其为一个平衡字符串。
现可以将 s 中连续的一段子串替换成相同长度的只包含那四个字符的任意字符串，使其变为一个平衡字符串，问替换子串的最小长度?

如果 s 已经平衡则输出0。
###  Input
一行字符表示给定的字符串s
###  Output
一个整数表示答案

### Examples
####  Input
```cpp
 QWER
```
#### Output
```cpp
 0
```
####  Input
```cpp
QQWE
```
#### Output
```cpp
1
```
####  Input
```cpp
QQQW
```
#### Output
```cpp
2
```
####  Input
```cpp
QQQQ
```
#### Output
```cpp
3
```
###  Note
$1<=n<=10^5$ , n是4的倍数. 字符串中仅包含字符``'Q', 'W', 'E' `` 和 ``'R'`` .
### Idea
我们需要寻找替换某个区间后，满足题目要求的条件的区间的集合中最小的那个，求解的答案区间是连续的，区间移动的时候长度会有所变化，该题就可以用尺取法。当替换区间满足要求就L++(因为在包含L元素的区间中没有比他更短的)，不满足就R++。
下面将需要满足的要转化为判断式。观察下图，需要保证区间大小>=差值部分之和，如果比它大，需要保证为4的倍数，这样才可以保证改变区间内的字符后满足要求。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324140146703.bmp?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYzMzE1Mw==,size_4,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20200324170152242.PNG)
###  Codes
```cpp
#include<iostream> 
#include<cstdio>
#include<cstring> 
using namespace std; 
int q,w,e,r,n,TOTAL,FREE,MAX,MIN;
string s;
bool check(int L,int R){
	int sum1=q,sum2=w,sum3=e,sum4=r; //q,w,e,r是四种字符的数量
	for(int i=L;i<=R;i++){   //用四种字符的数量-区间内的数量得到区间外的数量
		switch(s[i]){
    		case 'Q':  --sum1;break;
    		case 'W':  --sum2;break;
    		case 'E':  --sum3;break;
    		case 'R':  --sum4;break;
		}
	}
	MAX=sum1;       //找最大值
	if(MAX<sum2) MAX=sum2;
	if(MAX<sum3) MAX=sum3;
	if(MAX<sum4) MAX=sum4;
	TOTAL =R-L+1; 
	FREE=TOTAL-(4*MAX-sum1-sum2-sum3-sum4);
	if(FREE>=0 && FREE%4==0) return true;
	else return false;
} 
int main(){
    cin>>s;
    n=s.size();
    q=0, w=0, e=0, r=0;
    for(int i=0;i<n;i++){
    	switch(s[i]){
    		case 'Q':  q++;break;
    		case 'W':  w++;break;
    		case 'E':  e++;break;
    		case 'R':  r++;break;
		}
	}
    if(q==w && q==e && q==r) { cout<<"0"; }
	else{
	MIN =n+1;int L=0,R=0;
	while(L<n && R<n){
		if(check(L,R)){
		  if((R-L+1)<MIN) MIN=R-L+1;  
		  L++;	
		} 
		else {
			R++;
		}
	}
	cout<<MIN;
	}
	return 0;
} 
```
## Problem D-滑动窗口（C++和G++都交一下）
###  Description
ZJM 有一个长度为 n 的数列和一个大小为 k 的窗口, 窗口可以在数列上来回移动. 现在 ZJM 想知道在窗口从左往右滑的时候，每次窗口内数的最大值和最小值分别是多少. 例如：
数列是 [1 3 -1 -3 5 3 6 7], 其中 k 等于 3.
![ ](https://img-blog.csdnimg.cn/20200324114808158.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYzMzE1Mw==,size_16,color_FFFFFF,t_70)
###  Input
输入有两行。第一行两个整数n和k分别表示数列的长度和滑动窗口的大小，1<=k<=n<=1000000。第二行有n个整数表示ZJM的数列。
###  Output
输出有两行。第一行输出滑动窗口在从左到右的每个位置时，滑动窗口中的最小值。第二行是最大值。
### Sample Input
```cpp
8 3
1 3 -1 -3 5 3 6 7

```
###  Sample Output
```cpp
-1 -3 -3 -3 3 3
3 3 5 5 6 7
```
### Idea
滑动窗口长度固定，在长度内寻找最值。可以利用双端单调队列。用递增队列找最小值，递减队列找最大值。
从队尾插入新元素，如果新元素与对尾元素相比小(大)的话，就删除队尾元素，并继续比较新元素与尾元素，这样被删掉的元素比新元素大(小)，也会比新元素先离开窗口，就保证了队列的最小(大)值。
如果队首元素不在窗口时，就需要删去，需要维护数据的临时性。
###  Codes
```cpp
#include<iostream>
#include<cstdio>
#define MAX 1000050
using namespace std;
int A[MAX],que1[MAX],que2[MAX], n, k, s;
int front,back,size;
int main(){
	scanf("%d %d",&n,&k); 
	front=size=0;back=-1;
	for(int i=0;i<n;i++){
	 scanf("%d",&A[i]);  
	}
	for(int i=0;i<n;i++){
	   if(i>=k)	{
	   	  printf("%d ",que1[front]); 
		  if(que1[front] ==A[i-k]) {
		    ++front;  --size;
		  }   
	   }
	    while( size  &&  que1[back] >A[i])
		   {  
			--back; --size;
		   }
		que1[++back]=A[i];  ++size;
	}  
	printf("%d\n",que1[front]); 
	front=size=0; back=-1;	
	for(int i=0;i<n;i++){
		if(i>=k){ 
		  printf("%d ",que2[front]);
		  if(  que2[front] ==A[i-k])  {
		   ++front;--size;
	     }
		}
		while( size &&  que2[back] <A[i])
		{  
		  --back; --size;
		}
		que2[++back]=A[i];++size;
	}
    printf("%d\n",que2[front]);  
	return 0;
}
```
# 结束！     &nbsp;&nbsp;&nbsp;    [返回首页](./index.md)&nbsp;&nbsp;  [下篇Week6限时大模拟](./week6模拟.md) 
