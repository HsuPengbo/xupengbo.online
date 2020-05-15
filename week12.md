
## Problem A - 必做题 - 1
### Description
给出n个数，zjm想找出出现至少(n+1)/2次的数， 现在需要你帮忙找出这个数是多少？

### Input
本题包含多组数据：
每组数据包含两行。
第一行一个数字N(1<=N<=999999) ，保证N为奇数。
第二行为N个用空格隔开的整数。
数据以EOF结束。

### Output
对于每一组数据，你需要输出你找到的唯一的数。

### Sample Input
```
5
1 3 2 3 3
11
1 1 1 1 1 5 5 5 5 5 5
7
1 1 1 1 1 1 1
```
### Sample Output
```
3
5
1
```
### Idea
利用map结构{数，数量}，每次输入的数如果没有就插入，有的话就对其数量+1，最大数量的那个数就是答案。
### Codes
```cpp
#include<iostream>
#include<cstdio>
#include<map>
using namespace std;
int n,ans;
map<int,int> num;
int main(){ 
	pair<map<int,int>::iterator, bool> flag;
	map<int,int>::iterator it;
	int a;
	while(~scanf("%d",&n)){
		num.clear();
		for(int i=0;i<n;++i){
			scanf("%d",&a);
			flag=num.insert(pair<int,int>(a,1));
			if(flag.second==false){ 
				it=flag.first;
				(it->second)++;
			}
		}
		int max=-1;
		for(it=num.begin();it!=num.end();++it){
			if(max<(it->second)) {
			  max=it->second;	ans=it->first;
			}	
		}
		printf("%d\n",ans);
	}
	return 0;
} 
```
## Problem B - 必做题 - 2
### Description
zjm被困在一个三维的空间中,现在要寻找最短路径逃生！
空间由立方体单位构成。
zjm每次向上下前后左右移动一个单位需要一分钟，且zjm不能对角线移动。
空间的四周封闭。zjm的目标是走到空间的出口。
是否存在逃出生天的可能性？如果存在，则需要多少时间？

### Input
输入第一行是一个数表示空间的数量。
每个空间的描述的第一行为L，R和C（皆不超过30）。
L表示空间的高度，R和C分别表示每层空间的行与列的大小。
随后L层，每层R行，每行C个字符。
每个字符表示空间的一个单元。'#'表示不可通过单元，'.'表示空白单元。
zjm的起始位置在'S'，出口为'E'。每层空间后都有一个空行。
L，R和C均为0时输入结束。

### Output
每个空间对应一行输出。
如果可以逃生，则输出如下
Escaped in x minute(s).
x为最短脱离时间。

如果无法逃生，则输出如下
Trapped!

### Sample Input
```
3 4 5
S….
.###.
.##..
###.#

#####
#####
##.##
##…

#####
#####
#.###
####E

1 3 3
S##
#E#
###

0 0 0
```
### Sample Output
```
Escaped in 11 minute(s).
Trapped!
```
### Idea
刚开始用了DFS，发现我写的找到最小路径会超时，就换BFS+队列。
由于需要六个方向的判断，所以用循环的方式转向，对于每次转向后位置进行判断，满足边界条件并没有访问过才加入队列，并及时更新走过的距离+1。整个循环中找到终点就及时停止。
### Codes
```cpp
#include <iostream>
#include <cstring>
#include <cstdio> 
#include <queue>
using namespace std;
int L,R,C,ans; int si,sj,sk;
char Map[32][32][32];
bool vis[32][32][32]; 
int acti[]={1,-1,0,0,0,0};
int actj[]={0,0,1,-1,0,0};
int actk[]={0,0,0,0,1,-1};
struct pos{
	int i,j,k,d;
	bool Right(){
		if(i>=0 && i<L && j>=0 && j<R && k>=0 && k<C && vis[i][j][k]==false && Map[i][j][k]!='#'){
			vis[i][j][k]=true; return true; 
		}
		else return false;
	}
};
queue <pos> q;
void BFS(){
	while(!q.empty()) q.pop();
	pos po,pnew;  po.i=si;po.j=sj;po.k=sk;po.d=0;
	vis[si][sj][sk]=true;
	q.push(po);
	while(q.size()){
		po=q.front();q.pop();
		if(Map[po.i][po.j][po.k]=='E'){
			ans=po.d; break;
		} 
		for(int i=0;i<6;++i){
			pnew.i=po.i + acti[i];
			pnew.j=po.j + actj[i];
			pnew.k=po.k + actk[i];
			if(pnew.Right()){
				pnew.d=po.d+1;
				q.push(pnew); 
			}
		}
	}
}
void solve(){ 
	memset(vis,false,sizeof(vis));
	ans=0;
	for(int i=0;i<L;++i){
		for(int j=0;j<R;++j){
			for(int k=0;k<C;++k)
			 if(Map[i][j][k]=='S') {
			 	si=i;sj=j;sk=k;break;
			 } 
		}
	}
	BFS(); 
}
int main(){ 
	while(~scanf("%d%d%d",&L,&R,&C)){
	  if(L==0 && R==0 && C==0) return 0;
	  for(int i=0;i<L;++i){
	  	for(int j=0;j<R;++j){ 
		  	scanf("%s",&Map[i][j]);
		}
	  }
	  solve();	
	  if(ans==0) printf("Trapped!\n");
	  else printf("Escaped in %d minute(s).\n",ans);
	}
	return 0;
} 
```
## C - 必做题 - 3
### Description
东东每个学期都会去寝室接受扫楼的任务，并清点每个寝室的人数。
每个寝室里面有ai个人(1<=i<=n)。从第i到第j个宿舍一共有sum(i,j)=a[i]+...+a[j]个人
这让宿管阿姨非常开心，并且让东东扫楼m次，每一次数第i到第j个宿舍sum(i,j)
问题是要找到sum(i1, j1) + ... + sum(im,jm)的最大值。且ix <= iy <=jx和ix <= jy <=jx的情况是不被允许的。也就是说m段都不能相交。
注：1 ≤ i ≤ n ≤ 1e6 , -32768 ≤ ai ≤ 32767 人数可以为负数。(1<=n<=1000000)
### Input
输入m，输入n。后面跟着输入n个ai 处理到 EOF。
### Output
输出最大和。
### Sample Input
```
1 3 1 2 3
2 6 -1 4 -2 3 -2 3
```
### Sample Output
```
6
8 
```
### Hint
数据量很大，需要scanf读入和dp处理。
### Idea
一共需要分m组。
假如前j个宿舍一共分成i组,有最大和dp[i][j]
则可以发现状态转移规律:
dp[i][j]=max { dp[i][j-1], max(dp[i-1][k],1<= k <= j-1) }+A[j]
dp[i][j-1]+A[j]：前面j-1个数分成i组的最大值，把第j个宿舍放到最后一组中
dp[i-1][k]+A[j]：第j个宿舍单独放一组，前k个宿舍组成i-1组(前i-1组得最大值在每一轮都需要求一下保存下来，以便于后面使用)
### Codes
```cpp
#include<iostream>
#include<algorithm>
#include<cstdio>
using namespace std;
const int maxn=1000005;
const int inf=-1e9;
int m,n,ans;
int A[maxn],sum[maxn],dp[maxn];
void solve(){
	memset(sum,0,sizeof(sum));
	memset(dp,0,sizeof(dp));
	for(int i=1;i<=m;++i){
		ans=inf; 
		for(int j=1;j<=n;++j){
		  dp[i-1]=inf;
		  dp[j]=max(dp[j-1]+A[j],sum[j-1]+A[j]); sum[j-1]=ans;
		  ans=max(dp[j],ans);	 
		} 
	}
	printf("%d\n",ans);
}
int main(){ 
	while(~scanf("%d%d",&m,&n)){
	 for(int i=1;i<=n;++i)  scanf("%d",&A[i]);  
	 solve();
	}
	return 0;
}
```

