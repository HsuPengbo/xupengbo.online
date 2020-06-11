# 程序设计思维与实践 CSP-M4     [返回首页](./index.md)   [上篇 Week13](./week13.md)

## ProblemA - TT数鸭子

### Description

这一天，TT因为疫情在家憋得难受，在云吸猫一小时后，TT决定去附近自家的山头游玩。
TT来到一个小湖边，看到了许多在湖边嬉戏的鸭子，TT顿生羡慕。此时他发现每一只鸭子都不
一样，或羽毛不同，或性格不同。TT在脑子里开了一个map<鸭子，整数> tong，把鸭子变成了
一些数字。现在他好奇，有多少只鸭子映射成的数的数位中不同的数字个数小于k。
### Input
输入第一行包含两个数n,k，表示鸭子的个数和题目要求的k。
接下来一行有n个数,$a_i$，每个数表示鸭子被TT映射之后的值。
### Output
输出一行，一个数，表示满足题目描述的鸭子的个数。
无行末空格
### Sample Input
```cpp
6 5
123456789 9876543210 233 666 1 114514
```
### Sample Output
```cpp
4
```
### Note
![](https://blog.xupengbo.online/images/csp-m4-1.PNG?raw=true)

### Idea

### Codes
```cpp
#include<cstring>
#include<string>
#include<iostream>
using namespace std;
int n,k,ans; int p[10];
string num;
void check(){
	int siz=num.size(),cnt=0;
	memset(p,0,sizeof(p));
	for(int i=0;i<siz;++i)
		p[num[i]-'0']++;
	for(int i=0;i<10;++i)
		if(p[i]>0) cnt++;
	if(cnt<k) ans++;
}
int main(){
	std::ios::sync_with_stdio(false);
	ans=0;
	cin>>n>>k;
	for(int i=0;i<n;++i){
		cin>>num;
		check();
	}
	cout<<ans;
	return 0;
} 
```

## ProblemB - ZJM要抵御宇宙射线

### Description
据传，2020年是宇宙射线集中爆发的一年，这和神秘的宇宙狗脱不了干系！但是瑞神和东东忙
于正面对决宇宙狗，宇宙射线的抵御工作就落到了ZJM的身上。假设宇宙射线的发射点位于一个
平面，ZJM已经通过特殊手段获取了所有宇宙射线的发射点，他们的坐标都是整数。而ZJM要构
造一个保护罩，这个保护罩是一个圆形，中心位于一个宇宙射线的发射点上。同时，因为大部分
经费都拨给了瑞神，所以ZJM要节省经费，做一个最小面积的保护罩。当ZJM决定好之后，东东
来找ZJM一起对抗宇宙狗去了，所以ZJM把问题扔给了你~
### Input
输入 第一行一个正整数N，表示宇宙射线发射点的个数
接下来N行，每行两个整数X,Y，表示宇宙射线发射点的位置
### Output
输出包括两行
第一行输出保护罩的中心坐标x,y 用空格隔开
第二行输出保护罩半径的平方
（所有输出保留两位小数，如有多解，输出x较小的点，如扔有多解，输入y较小的点）
无行末空格
### Sample Input
```cpp
5
0 0
0 1
1 0
0 -1
-1 0
```
### Sample Output
```cpp
0.00 0.00
1.00
```
### Note

![](https://blog.xupengbo.online/images/csp-m4-2.PNG?raw=true)

### Idea

### Codes
```cpp
#include<iostream>
#include<cstdio>
#include<algorithm>
#include<cmath>
#include<cstring>
#define ll long long
using namespace std;
const int maxn=1001;
const ll inf=1e15;
int N;double R;
struct Point{
	ll x,y;
	bool operator<(Point t){
		if(x!=t.x) return x<t.x;
		else y<t.y;
	}
}ans;Point points[maxn];
ll dis(Point a,Point b){
	return (a.x-b.x)*(a.x-b.x)+(a.y-b.y)*(a.y-b.y);
}
void solve(){
	sort(points,points+N);
	ll d=0,maxd=0,R=inf;
	for(int i=0;i<N;++i){
		maxd=0;
		for(int j=0;j<N;++j){
			d=dis(points[i],points[j]);
			if(d>maxd) maxd=d;
		}
		if(R>maxd) {
		 R=maxd;	ans=points[i];
		}
	}
	printf("%lld.00 %lld.00\n",ans.x,ans.y);
	printf("%lld.00",R);
}
int main(){
	scanf("%d",&N);
	for(int i=0;i<N;++i){
		scanf("%lld %lld",&points[i].x,&points[i].y);
	}
	solve();
	return 0;
} 
```

## ProblemC - 宇宙狗的危机
时间限制 空间限制
5S 256MB
### Description
在瑞神大战宇宙射线中我们了解到了宇宙狗的厉害之处，虽然宇宙狗凶神恶煞，但是宇宙狗有一
个很可爱的女朋友。
最近，他的女朋友得到了一些数，同时，她还很喜欢树，所以她打算把得到的数拼成一颗树。
这一天，她快拼完了，同时她和好友相约假期出去玩。贪吃的宇宙狗不小心把树的树枝都吃掉
了。所以恐惧包围了宇宙狗，他现在要恢复整棵树，但是它只知道这棵树是一颗二叉搜索树，同
时任意树边相连的两个节点的gcd(greatest common divisor)都超过1。
但是宇宙狗只会发射宇宙射线，他来请求你的帮助，问你能否帮他解决这个问题。
补充知识：
GCD：最大公约数，两个或多个整数共有约数中最大的一个 ，例如8和6的最大公约数是2。
一个简短的用辗转相除法求gcd的例子：
int gcd(int a,int b){return b == 0 ? a : gcd(b,a%b);}
### Input
输入第一行一个t，表示数据组数。
对于每组数据，第一行输入一个n，表示数的个数
接下来一行有n个数ai，输入保证是升序的。
### Output
每组数据输出一行，如果能够造出来满足题目描述的树，输出Yes，否则输出No。
无行末空格。
### Sample Input 1
```cpp
1
6
3 6 9 18 36 108
```
### Sample Output 1
```cpp
Yes
```
### Sample Input 2
```cpp
2
2
7 17
9
4 8 10 12 15 18 33 44 81
```
### Sample Output 2
```cpp
No
Yes
```
### Sample Explain
样例1可构造如下图
![](https://blog.xupengbo.online/images/csp-m4-4.PNG?raw=true)
### Note
![](https://blog.xupengbo.online/images/csp-m4-3.PNG?raw=true)
### Idea
由于输入的序列Node[  ]为升序序列,所以假如存在满足条件的二叉树时,必然有根节点Node[p]满足:Node[1,p-1]为Node[p]左子树,Node[p+1,n]为p右子树。

设置数字Root[i][j]表示区间[i,j]的根情况,如果=true，说明点i到j之间存在一个根p(i<=p<=j)使其为二叉树,如果=false说明不存在根节点使其形成一个二叉树。

我们再设置L[l][p],R[p][r],L[l][p]=true表示l到p-1属于p的左子树,R[p][r]=true表示p+1到r属于p的右子树.

对于本身就可以连接的两点i和j(i<=j)，i天然可以作为j的左子树(i!=j表示只有一个左子节点,i==j说明左子节点为空,j天然的可以作为i的右子树。
满足连接的条件就是题目给定的两点的数之间最大公约数>1。

状态转移:
如果对于L[l][p]==true&& R[p][r]==true,说明从l到r存在一个根节点让其成为一个二叉树,则令Root[l][r]=true。
如果p和r+1也能连接，则说明p可以做r+1的左子节点，那么此时存在的从l到r的树就是r+1的左子树，就及时更新L[l][r+1]=true。
R[l-1][r]同理判断是否更新为true。
### Codes
```cpp
#include<cstdio>
#include<cstring>
using namespace std;
int t,n;
int gcd(int a,int b){return b == 0 ? a : gcd(b,a%b);}
int node[705]; bool Root[705][705],L[705][705],R[705][705],Lines[705][705];
void init(){
	memset(L,false,sizeof(L));
	memset(R,false,sizeof(R));
	memset(Root,false,sizeof(Root));
 	memset(Lines,false,sizeof(Lines));
 	for(int i=1;i<=n;++i){
 		L[i][i]=true; R[i][i]=true;
	 }
}
void gcdLine(int i,int j){
	if(gcd(node[i],node[j])>1) {
		Lines[i][j]=Lines[j][i]=true;
	}
}
void NodeToTree(){ 
	for(int i=1;i<=n;++i){
		for(int j=1;j<=n;++j){
		 gcdLine(i,j);
		} 
	}
	for(int T=1;T<=n;++T){
		for(int l=1,r=l+T-1; r<=n; ++l,++r){//从[1,1]...[n,n];[1,2]...[n-1][n];[1,3]...循环遍历到区间[1~n] 
			for(int p=l;p<=r;++p){
				if(L[l][p] && R[p][r]) {
					Root[l][r]=true; 
					if(Lines[p][r+1])L[l][r+1]=true; //r+1与p节点如果可以相连,则存在p为其左子节点的左子树 
					if(Lines[p][l-1])R[l-1][r]=true; //l-1与p节点如果可以相连,则存在p为其右子节点的右子树
				}  
			}
		}
	}
	if(Root[1][n]) printf("Yes\n");
	else printf("No\n");
} 
void solve(){
	scanf("%d",&t);
	for(int i=0;i<t;++i){
		scanf("%d",&n);init();
		for(int j=1;j<=n;++j){
			scanf("%d",&node[j]);
		}
		NodeToTree();
	}
}
int main(){
	solve();
	return 0;
}
```

# 结束!     [返回首页](./index.md)   [下篇 元素选择器](./CSP-201809-3.md)
