#  第四周习题          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       [返回首页](./index.md)&nbsp;&nbsp;  [上篇 CSP-M1](./CSP-M1.md)
## Problem A - DDL 的恐惧
### Description
ZJM 有 n 个作业，每个作业都有自己的 DDL，如果 ZJM 没有在 DDL 前做完这个作业，那么老师会扣掉这个作业的全部平时分。所以 ZJM 想知道如何安排做作业的顺序，才能尽可能少扣一点分。请你帮帮他吧！
###  Input
输入包含T个测试用例。输入的第一行是单个整数T，为测试用例的数量。
每个测试用例以一个正整数N开头(1<=N<=1000)，表示作业的数量。
然后两行。第一行包含N个整数，表示DDL，下一行包含N个整数，表示扣的分。
###  Output
对于每个测试用例，您应该输出最小的总降低分数，每个测试用例一行。
### Example
#### Input
```cpp
3
3
3 3 3
10 5 1
3
1 3 1
6 2 3
7
1 4 6 4 2 4 3
3 2 1 7 6 5 4
```
#### Output
```cpp
0
3
5
```
### Idea
贪心算法   
数据结构：先建立DDL结构 { 时间，扣分 }。重定义<为扣分大的优先。   
处理：输入DDL的所有数据后，把数组先按优先级排序。初始数组vis[N]为false，都没有访问过。   
初始ans=所有score分数（对于每个元素，都先假设不能满足条件） 
之后遍历所有的元素，对每个DDL，从给定deadline开始递减，观察是否有vis[i]未被访问(处于空闲状态)。如果在它之前的都被访问说明前面有更分数更大的DDL要做；如果存在未被访问的时间点，就说明可以安排上，ans再减去对应的分数。
最终剩下的分数就是没有按时完成的最小代价。
###  Codes
```cpp
#include<iostream> 
#include<algorithm>
#include<cstring>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std; 
int T;int N;   
struct DDL{                                                   //结构
	int time;
	int score;
	bool operator<(DDL z ){
		if(score>z.score) return true;
		else return false;
	}
}; 
DDL *D;
bool vis[1002]={false};
int main(){
    cin>>T; int ans=0;
    _for(i,0,T){
       while(cin>>N){
       	   ans=0;
       	   memset(vis,false,sizeof(vis));               
       	   D= new DDL[N];
       	   _for(j,0,N)  cin>>D[j].time; 
		   _for(j,0,N){  cin>>D[j].score; ans+=D[j].score;}  //ans把所有输入的分数都加上
		   sort(D,D+N);                                      //先根据score排序
		   _for(j,0,N)
			  for(int p=D[j].time;p>=1;p--){
				  if(!vis[p]){
					vis[p]=true; 
					ans-=D[j].score;                         //该DDL可以被安排，把对应分数减掉
					break;
				   }
			   } 
		    cout<<ans<<endl;                                 //输出剩余的没有完成的任务的分数之和
	  }
  } 
	return 0;
}
```
## Problem  B - 四个数列
### Description
ZJM 有四个数列 A,B,C,D，每个数列都有 n 个数字。ZJM 从每个数列中各取出一个数，他想知道有多少种方案使得 4 个数的和为 0。当一个数列中有多个相同的数字的时候，把它们当做不同的数对待。请你帮帮他吧！
### Input
第一行：n（代表数列中数字的个数） （1≤n≤4000）
接下来的 n 行中，第 i 行有四个数字，分别表示数列 A,B,C,D 中的第 i 个数字（数字不超过 2 的 28 次方）
### Output
输出不同组合的个数。
### Example
#### Input
```cpp
6
-45 22 42 -16
-41 -27 56 30
-36 53 -37 77
-36 30 -75 -46
26 -38 -10 62
-32 -54 -6 45
```
#### Output
```cpp
5
```
### Idea
二分法的应用：    
分析A，B，C，D四个数列各取出一个数相加和为0，    
即a+b+c+d=0  ->  a+b=-(c+d)，左边两个数列二重循环计算所有可能的和，右边两个数列也计算所有的和，计算相等的情况。       
也就是左边二重循环计算和，然后sort()排序。然后右边两个数列各取数相加的二重循环中，查找A+B中有多少个相反的数。用到两个函数，查找第一个大于等于该数的位置和最后以一个小于等于该元素的位置。右-左+1就是该数在A+B中的个数，也就是多少种情况。   
###  Codes
```cpp
#include <iostream> 
#include <algorithm>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;  
int N,n;
const int MAX=4002;
int A[MAX] , B[MAX] ,C[MAX] ,D[MAX];
int AB[MAX*MAX]; 
int find_first(int *a,int n,int x)//找到某元素第一次出现位置(数组，长度，元素)
{
  int l=0,r=n-1,ans=-1;
  while(l<=r){
  	int mid=(l+r)>>1;
  	if(a[mid]==x){
  		ans =mid; 
  		r=mid-1;
	  }
	else if(a[mid]>x) r=mid-1;
	else l=mid+1;
  } 
    return ans; 
} 
int find_last(int *a,int n,int x) 
{
  
  int l=0,r=n-1,ans=-1;
  while(l<=r){
  	int mid=(l+r)>>1;
  	if(a[mid]==x){
  		ans =mid;
  		l=mid+1;
	  } 
	else if(a[mid]<x) l=mid+1;
	else r=mid-1;
  }  
    return ans;
}  
void getSum(){
	int sum=0,n;
	_for(i,0,N)
	  _for(j,0,N) 
	  	AB[n++]=A[i]+B[j];  
	sort(AB, AB + n);	
	int x,cnt1,cnt2,cnt;
	_for(i,0,N){
		_for(j,0,N){
			int x= (C[i]+D[j])*(-1);
		   cnt1=find_last(AB,n,x); 
		   cnt2=find_first(AB,n,x); 
		   cnt = cnt1-cnt2 + 1;
		   if(cnt1>-1) sum +=cnt; 
		}	
	} 
    cout<<sum<<endl;
}
int main(){ 
   	cin>>N; 
   _for(i,0,N){
   	 cin>>A[i]>>B[i]>>C[i]>>D[i];
   } 
   getSum(); 
	return 0;
}
```
## Problem C - TT 的神秘礼物
### Description
TT 是一位重度爱猫人士，每日沉溺于 B 站上的猫咪频道。

有一天，TT 的好友 ZJM 决定交给 TT 一个难题，如果 TT 能够解决这个难题，ZJM 就会买一只可爱猫咪送给 TT。

任务内容是，给定一个 N 个数的数组 cat[i]，并用这个数组生成一个新数组 ans[i]。新数组定义为对于任意的 i, j 且 i != j，均有 ans[] = abs(cat[i] - cat[j])，1 <= i < j <= N。试求出这个新数组的中位数，中位数即为排序之后 (len+1)/2 位置对应的数字，'/' 为下取整。
### Input
TT 非常想得到那只可爱的猫咪，你能帮帮他吗？
### Output
多组输入，每次输入一个 N，表示有 N 个数，之后输入一个长度为 N 的序列 cat， cat[i] <= 1e9 , 3 <= n <= 1e5
### Example
#### Input
```cpp
4
1 3 2 4
3
1 10 2
```
#### Output
```cpp
1
8
```
### Idea
该题仍然是二分法的一种应用。分析题意，就是对一个数组自身两个下标不同的元素差的绝对值形成的数组，求其中位数。   
如果把该数组先从小到大排序后，总有右-左>0，且我们还知道新数组中最大的数是原数组最右端与最左端的差值。最小差值也大于等于0。如果我们把所有的绝对值都算出来再排序，然后找中位数，复杂度太大,为O(N^2).     
如果用二分法，假设``right=A[N-1]-A[0] , left=0``，设所求中位数为``mid``。刚开始``mid``可以取为``(left+right)/2``。    
那我们只需要判断mid取得是否合适，二分法不断迭代。由于``A[j]-A[i]=cnt即 A[j]=A[i]+cnt``，那每次只需要遍历从``i=0``到``N-1``，去计算从``A[ i+1]``处到``A[N-1]``处存在多少个小于``mid+A[i]``的数(用``lower_bound()``函数)，如果相加大于``newN/2``说明中位数取得大了，反之说明取得小了。这样复杂度就变成了 
![](https://github.com/HsuPengbo/HsuPengbo.github.io/blob/master/00002.png) 。
当N=1e9,Right=1e5时，
![](https://github.com/HsuPengbo/HsuPengbo.github.io/blob/master/00002.png) 
≈496.584N   
`` 注意：newN=N(N-1)/2, 有一半差的绝对值都是重复。``
###  Codes
```cpp 
#include <iostream>
#include <cstdio>
#include <algorithm>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;  
long long N, newN;
int A[100002];
bool Low(int mid)// 判断mid取的大小 
{
	long long cnt = 0;
	_for(i,0,N)
	{
		cnt += A + N - lower_bound(A + i + 1, A + N, mid + A[i]);	// 返回小于 mid+A[i] 的元素数目
		if(cnt>newN/2) return false; 
	}
	return cnt <= newN / 2;
}
int main()
{ 
	while (~scanf("%d",&N))
	{
		_for(i,0,N) {
			scanf("%d",&A[i]);
		}
		sort(A, A + N);
		newN = N*(N - 1)/2;
		int l = 0, r = A[N-1] - A[0];
		while (r - l > 1)
		{
			int mid = (l + r) >> 1;
			if (Low(mid))	r = mid;
			else	l = mid;
		}
		printf("%d\n",l);
	} 
	return 0;
}
```
# 结束！    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       [返回首页](./index.md)&nbsp;&nbsp;  [下篇 待定]
