## Problem A - 选数问题
####   Description
Given n positive numbers, ZJM can select exactly K of them that sums to S. Now ZJM wonders how many ways to get it!

####  Input
The first line, an integer T<=100, indicates the number of test cases. For each case, there are two lines. The first line, three integers indicate n, K and S. The second line, n integers indicate the positive numbers.
####  Output
For each case, an integer indicate the answer in a independent line.
####  Sample Input
```
1
10 3 10
1 2 3 4 5 6 7 8 9 10
```
####  Sample Output
```
4
```
####  Note
```
Remember that k<=n<=16 and all numbers can be stored in 32-bit integer
```
####  Idea
 [DFS] 先定义一个变量t=0。对所有的数遍历，选是一种情况，不选是一种情况，然后分别向下一层搜索。满足条件的话，返回t++。如果选的数超过限度或者和大于输入值停止。最后所有的成功情况都会对t+1，得到的t值就是答案。
####  Codes
 |   |   |  |  |   |     
 |--|-- |-- |--|--|
 | Time | Memory | Length | Lang | Submitted |
 |   265ms | 140kB | 588  | GNU G++17 7.3.0 | 2020-03-05 14:30:27 |  
```cpp
#include<iostream>
#include <list>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;
int List[16]={0}; 
int n,K,S;int t;
list<int> res;
void Gets(int i,int sum,list<int> &res){
	if(res.size()==K && sum==0){
	   t++; return;
	}
	if(i>=n) return;
	if(res.size()>K ||sum<0) return;
	Gets(i+1,sum,res);
	res.push_back(List[i]);
	Gets(i+1,sum-List[i],res);
	res.pop_back();
}
void getWays(int n,int K,int S){
	_for(i,0,n){
		cin>>List[i];
	}
	t=0;
    Gets(0,S,res);
	cout<<t<<endl;
}
int main(){
	int T;cin>>T;
	while(T--){
		cin>>n>>K>>S;
		getWays(n,K,S);
	}
	
	return 0;
} 
```
## Problem B- 区间选点
####    Description
数轴上有 n 个闭区间 [a_i, b_i]。取尽量少的点，使得每个区间内都至少有一个点（不同区间内含的点可以是同一个）
####  Input
第一行1个整数N（N<=100）
第2~N+1行，每行两个整数a,b（a,b<=100）
####  Output
一个整数，代表选点的数目
####  Input 
```
2
1 5
4 6
```
**Output**
```
1
```
**Input** 
```
3
1 3
2 5
4 6
```
**Output**
```
2
```
####  Idea
贪心策略： 按照<右端小的在前，右端一样的左端小的在前>规则，对输入的所有区间进行排序。然后从头遍历每个区间。初始sum=0，定义一个临时变量cnt作为循环中的右端点(初始为第一个区间右端点)，每次观察下一个区间左端点是否与当前 cnt相交，不相交的话就sum+1(说明需要取新的点)，并更新cnt为其右端点 (相交的话用当前的右端点就够了)。
####  Codes
 |   |   |  |  |   |  
 |--|-- |-- |--|--|
 | Time | Memory | Length |  Lang | Submitted |
 |  15ms   |   8kB  |   814    | GNU G++17 7.3.0| G++   |    2020-03-05 15:06:32   |   
```cpp
#include<iostream>
#include <list>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;
int sum=0,N;
struct Pair{
	int a,b;
	bool operator<(Pair X){
		if(X.b==b) return a<X.a;
		return b<X.b;
	}
}; Pair M[100];
void ShellSort(Pair A[],int n){
    int i, j,cnt;
	Pair tmp; 
    for (cnt = n/ 2; cnt > 0; cnt /= 2) {    
        for (i = cnt; i < n; i++) {  
            tmp = A[i];  
            for (j = i - cnt; j >= 0 && tmp < A[j]; j -= cnt) {  
                A[j + cnt] = A[j];  
            }  
            A[j + cnt] = tmp;
        }  
    }
}
void getSum(){
	_for(i,0,N){
		cin>>M[i].a>>M[i].b;
	}
	ShellSort(M,N);
	sum=1;
	int cnt=M[0].b;
	for(int i = 1; i < N; i++){
		if(M[i].a > cnt) {  
		cnt = M[i].b;
		sum++;
	    }
	}
	cout<<sum<<endl;
}
int main(){
	cin>>N;
	getSum();
	return 0;
}
```
## Problem C - 区间覆盖
####    Description
数轴上有 n (1<=n<=25000)个闭区间 [ai, bi]，选择尽量少的区间覆盖一条指定线段 [1, t]（ 1<=t<=1,000,000）。
覆盖整点，即(1,2)+(3,4)可以覆盖(1,4)。
不可能办到输出-1
####  Input
 第一行：N和T
 第二行至N+1行: 每一行一个闭区间。
####  Output
选择的区间的数目，不可能办到输出-1
####  Sample Input 
```
3 10
1 7
3 6
6 10
```
#### Sample Output
```
2
```
####  Note
这道题输入数据很多，请用scanf而不是cin
####  Idea
贪心策略：先按左端点大小升序，再按右端点升序。这样即便有被包括的区间，小也会被放在前面，不影响更新--->把1作为初始Start(左端点)和End(右端点)，每次从当前区间向后遍历，遇到最后一个左端点<start右端点>End的，把End作为当前End,Start取下一个点(End+1)，Sum++，然后向后接着观察及更新。需要注意终止循环的边界条件。由于我用的for循环最后一步没法向后走了，所以需要在循环外加一句判断，如果End>T，就输出sum+1反之输出-1.
####  Codes
 |   |   |  |  |   |     
 |--|-- |-- |--|--|
 | Time | Memory | Length | Lang | Submitted |
 |  63ms | 836kB | 810  | G++ | 2020-03-06 14:10:30 |  
    
```cpp
#include<cstdio>
#include<iostream>
#include<algorithm>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;
const int MAX=1<<20;
struct Node{
	int a,b;
}; 
bool cmp(Node X,Node Y){
		if(X.a==Y.a) return X.b<Y.b;
		return X.a<Y.a;
	}
Node M[MAX]; int Start, End,N,T; bool Tag=true;
int main(){
	
	while(scanf("%d%d",&N,&T)!=EOF){
    int sum=0;Tag=true;
	_for(i,0,N){	 
	scanf("%d%d",&M[i].a, &M[i].b); 
	} 
	sort(M,M+N,cmp);
	if(M[0].a>1)  {  puts("-1"); continue; } 
	Start=1,End=1;  int nEnd=1;
    _for(i,0,N){
		if(M[i].a<=Start && M[i].b>End){
    		End=M[i].b;	
		}
        if(M[i].a>Start){
        	if(M[i].a>End+1) {
			 Tag=false;break;
			} 
			Start=End+1; sum++; i--; 
		}
		if(End>=T) break;
	}
	if(End<T ||Tag==false)   {  puts("-1");} 
	else printf("%d\n",sum+1);
	}
	return 0;
} 
```
