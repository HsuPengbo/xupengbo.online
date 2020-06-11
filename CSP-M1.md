#  CSP-M1 习题    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       [返回首页](./index.md)&nbsp;&nbsp;  [上篇 week4](./week4.md)
## Problem A - 咕咕东的奇遇
### Description
咕咕东是个贪玩的孩子，有一天，他从上古遗迹中得到了一个神奇的圆环。这个圆环由字母表组成首尾相接的环，环上有一个指针，最初指向字母a。咕咕东每次可以顺时针或者逆时针旋转一格。例如，a顺时针旋转到z，逆时针旋转到b。咕咕东手里有一个字符串，但是他太笨了，所以他来请求你的帮助，问最少需要转多少次。 
### Example
#### Input
```cpp
hzet
```
#### Output
```cpp
31
```
### Idea
这道题是一个比较简单的模拟题，转盘初始字母为a,之后根据每次输入的字母可以不断计算该字母在转盘里与上一个字母的距离，可以用字母本身的ASCII值作差，取``绝对值``与``26-绝对值``比较,哪个小哪个就是最短距离。累计距离的和就是需要转的次数。
###  Codes
```
#include<iostream> 
#include<cmath>
#include<cstring>
using namespace std;
int Len(char s,char t){
	int L=(s-t);
	L=abs(L);
	return (L< 26-L)? L:26-L;
}
int main(){
	string str;cin>>str;
	int L=str.length(); int sum=0;
	sum+=Len(str[0],'a'); 
	for(int i=0;i<L-1;i++){
		sum+=Len(str[i],str[i+1]); 
	}
	cout<<sum<<endl;
	return 0;
}
```
##  B - 咕咕东想吃饭
### Description
咕咕东考试周开始了，考试周一共有n天。他不想考试周这么累，于是打算每天都吃顿好的。他决定每天都吃生煎，咕咕东每天需要买ai个生煎。但是生煎店为了刺激消费，只有两种购买方式：①在某一天一次性买两个生煎。②今天买一个生煎，同时为明天买一个生煎，店家会给一个券，第二天用券来拿。没有其余的购买方式，这两种购买方式可以用无数次,但是咕咕东是个节俭的好孩子，他训练结束就走了，不允许训练结束时手里有券。咕咕东非常有钱，你不需要担心咕咕东没钱，但是咕咕东太笨了，他想问你他能否在考试周每天都能恰好买ai个生煎。 
### Example
#### Input
```
4
1 2 1 2
```
#### Output
```
YES
```
### Idea
数据输入处理：
从数据中可以看出，除了第i天本身为A[i]=0外所有的数都可以看作只有1和2的数列，因为大于2的数都可以不断减去2(方案1)，但是A[i]=2时不一定选择方案1，所以需要保留。
分析券q和要买的包子数量A[i]情况（q,A[i])：

|当前步(q,A[i]) | 下一步(q,A[i+1]) |备注 |
|---|---|---|
|0,0| 0,A[i+1] |情况①|
|0,1| 1,A[i+1] |情况②|
|0,2| 0,A[i+1] |情况①|
|1,0| `` return`` |可以表示为``q>A[i]``|
|1,1| 0,A[i+1]| 情况①|
|1,2| 1,A[i+1]|情况②|

思路：
DFS递归处理，设``sum=0``, 递归函数中设 ``q`` (当前拥有券的数量), ``i`` (当前步数)
```
Buy( int *a,int i,int q)
```
边界条件：当``i``遍历到N说明有成功的情况，``sum++``。如果最后发现``sum>0``就知道有成功的方案
剪去条件：当``q>1``或者 ``q>A[i]``时中断
递归判断：
+  情况①：``(q^A[i])%2==0`` . ``//只是想把同一种情况的放进一个式子判断,没有什么实际价值``
```
Buy(a,i+1,0)
```
+  情况②：``(q^A[i])%2==1``
```
Buy(a,i+1,1)
```

###  Codes

```
#include<iostream> 
using namespace std;
int N,sum;
const int MAX=100000;
int A[MAX]={0};
void input() //对输入的数进行处理
{
	cin>>N;
	for(int i=0;i<N;i++){
		cin>>A[i];
		if(A[i]>0){
			A[i]=(A[i]%2==0)?2:1;
		}
	}
	sum=0;
}
void output(){
	if(sum>0) cout<<"YES"<<endl;
	else cout<<"NO"<<endl;
}
void Buy(int *a,int i,int q){
	if(i==N) {
		if(q==0) sum++;
		return;
	}	
	int t=a[i];
	if(q>1 || q>t) return;
    else if((q^t)%2==0) Buy(a,i+1,0); 
	else Buy(a,i+1,1);
}
 
int main(){
	input();
	Buy(A,0,0);
	output();
	return 0;
}
```

##  C - 可怕的宇宙射线

### Description
众所周知，瑞神已经达到了CS本科生的天花板，但殊不知天外有天，人外有苟。在浩瀚的宇宙中，存在着一种叫做苟狗的生物，这种生物天生就能达到人类研究生的知识水平，并且天生擅长CSP，甚至有全国第一的水平！但最可怕的是，它可以发出宇宙射线！宇宙射线可以摧毁人的智商，进行降智打击！
宇宙射线会在无限的二维平面上传播（可以看做一个二维网格图），初始方向默认向上。宇宙射线会在发射出一段距离后分裂，向该方向的左右45°方向分裂出两条宇宙射线，同时威力不变！宇宙射线会分裂n次，每次分裂后会在分裂方向前进ai个单位长度。
现在瑞神要带着他的小弟们挑战苟狗，但是瑞神不想让自己的智商降到普通本科生那么菜的水平，所以瑞神来请求你帮他计算出共有多少个位置会被"降智打击" 

### Example

#### Input

```
4
4 2 2 3
```
#### Output

```
39
```

### Idea

这道题用DFS+记忆化。
+ 前提和假设
方向``dir[8]``,位置``map[300][300]``,距离dis,给定每步距离``Dis[31]``。状态用`` status[step][x][y][dir][dis]``表示，即每个点``(x,y)``在第``step``步处于``dir``方向，还剩``dis``距离需要前进。方向用``dx[],dy[]``共同表示,按从上顺时针表示为``(0,1)、(1,1)、(1,0)···(-1,1)``。当前方向的左倾方向为``(dir+7)%8``,右为``(dir+9)%8``。
+ 递归思路
如果step超过了给定的N,或者当前状态已经被访问就return,如果该点没有经历过就sum++。
然后给状态和点的访问都标记。然后判断如果还需要前进就前进一格，进入(x,y,dir,dis,step)
不然就分左倾和右倾递归。

###  Codes

```
#include<iostream>
#include<cstring>
#include<cstdio>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;

const int MAX=300;
int Dis[31]={0};
int N,sum=0; 
const int dx[8]={0,1,1,1,0,-1,-1,-1};//x变化 
const int dy[8]={1,1,0,-1,-1,-1,0,1};//y变化 
bool map[MAX][MAX]={false};
bool status[30][MAX][MAX][8][6]={false};// Position:x,y; Direction:0-7; Remaining Distance:0-5

void visitDFS(int x,int y,int dir,int dis,int step){
	if(step>N-1) return;
	if(status[step][x][y][dir][dis])return;
	if(!map[x][y]) 	  sum++;
	map[x][y]=true; status[step][x][y][dir][dis]=true;
	if(dis>0){
	  x+=dx[dir];y+=dy[dir];dis--;
	  visitDFS(x,y,dir,dis,step);	
	} 
	else if(step<N-1){
	int dir1= (dir+7)%8, dir2= (dir+9)%8;
	int dx1=dx[dir1],dx2=dx[dir2],dy1=dy[dir1],dy2=dy[dir2];
	int dis1=Dis[step+1]-1,dis2=Dis[step+1]-1;
	visitDFS(x+dx1, y+dy1, dir1, dis1, step+1);
	visitDFS(x+dx2, y+dy2, dir2, dis2, step+1);	
	}
	return;
}
void input(){
	scanf("%d",&N);
	_for(i,0,N){
		scanf("%d",&Dis[i]);
	}  
}
void Visit(){
	int dis=Dis[0]-1;
	sum=0;
	visitDFS(150,150,0,dis,0);
}
void output(){
	printf("%d",sum);
}
int main(){
	input();
	Visit();
	output();
	return 0;
}
```

# 结束！&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       [返回首页](./index.md) &nbsp;&nbsp;  [下篇 画图](./CSP-201512-3.md)
