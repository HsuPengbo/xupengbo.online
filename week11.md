#  程序设计思维与实践第十一周  [返回首页](./index.md) [上篇week10作业+限时模拟](./week10.md)

## Problem A-买房子

### Description 
蒜头君从现在开始工作，年薪 NN 万。他希望在蒜厂附近买一套 6060 平米的房子，现在价格是 200200 万。假设房子价格以每年百分之 KK 增长，并且蒜头君未来年薪不变，且不吃不喝，不用交税，每年所得 NN 万全都积攒起来，问第几年能够买下这套房子？（第一年年薪 NN 万，房价 200 万）
 
### Input  
一行，包含两个正整数 N(10≤N≤50)，K(1≤K≤20)，中间用单个空格隔开。
 
### Output 
如果在第 2020 年或者之前就能买下这套房子，则输出一个整数 MM，表示最早需要在第 MM 年能买下；否则输出"Impossible"。
输出时每行末尾的多余空格，不影响答案正确性

### Sample Input 
 
```
50 10
``` 
 
### Sample Output  
 ```
 8
 ``` 
### Idea
这道题很简单，就是拿每年房子的房价和年薪积累和比较，如果20年内都不能买就认为不可能。

### Codes
```
#include<iostream>
#include<cstdio>
using namespace std;
int N,K;
void solve(){
	bool ok=false;
	double all=200.0;int i=0;
	for(i=1;i<21;++i){ 
	    if(i>1)   	all=all*(1 + K/100.0); 
		if(all<=N*i) { ok=true; break; }
	}
	if(ok) printf("%d",i);
	else printf("Impossible");
}
int main(){
	scanf("%d%d",&N,&K); 
	solve();
} 
```

## Problem B-蒜头君列队 

### Description 
蒜头君的班级里有 n^2n2 个同学，现在全班同学已经排列成一个 n * nn∗n 的方阵，但是老师却临时给出了一组新的列队方案
为了方便列队，所以老师只关注这个方阵中同学的性别，不看具体的人是谁
这里我们用 00 表示男生，用 11 表示女生
现在蒜头君告诉你同学们已经排好的方阵是什么样的，再告诉你老师希望的方阵是什么样的
他想知道同学们已经列好的方阵能否通过顺时针旋转变成老师希望的方阵

```
不需要旋转则输出 00
顺时针旋转 90° 则输出 11  
顺时针旋转 180° 则输出 22  
顺时针旋转 270° 则输出 33  
若不满足以上四种情况则输出 -1−1  
若满足多种情况，则输出较小的数字  
```

### Input
第一行为一个整数 nn  
接下来的 nn 行同学们已经列好的 0101 方阵；  
再接下来的 nn 行表示老师希望的的 0101 方阵。  

### Output
输出仅有一行，该行只有一个整数，如题所示。

### Sample Input
```
4
0 0 0 0
0 0 0 0
0 1 0 0
0 0 0 0
0 0 0 0
0 1 0 0
0 0 0 0
0 0 0 0
```
### Sample Output

```
1
```

### Idea
就是拿初始矩阵和变换后矩阵比较，
```
不旋转:A[i][j]=B[i][j]
旋转90度:A[i][j]=B[j][N-1-i]
旋转180度:A[i][j]=B[N-1-i][N-1-j]
旋转270度:A[i][j]=B[N-1-j][i]
```

### Codes
```cpp
#include<iostream>
#include<cstdio>
using namespace std;
int A[21][21],B[21][21];
int N;
void solve(){
	bool f0=true,f1=true,f2=true,f3=true;
	for(int i=0;i<N;++i) 
	  for(int j=0;j<N;++j)
	  {
	  	if(A[i][j]!=B[i][j]) f0=false;
	  	if(A[i][j]!=B[j][N-1-i]) f1=false;
	  	if(A[i][j]!=B[N-1-i][N-1-j]) f2=false;
	  	if(A[i][j]!=B[N-1-j][i]) f3=false;
	  }
	if(f0) printf("0");
	else if(f1)printf("1");
	else if(f2)printf("2");
	else if(f3)printf("3");
	else printf("-1");
}
int main(){
	scanf("%d",&N);
	for(int i=0;i<N;++i) 
	  for(int j=0;j<N;++j)
	    scanf("%d",&A[i][j]);
	for(int i=0;i<N;++i) 
	  for(int j=0;j<N;++j)
	    scanf("%d",&B[i][j]);
	solve();
} 
```

## Problem C-简单密码
### Description
Julius Caesar 曾经使用过一种很简单的密码。对于明文中的每个字符，将它用它字母表中后 55 位对应的字符来代替，这样就得到了密文。比如字符'A'用'F'来代替。如下是密文和明文中字符的对应关系。
密文
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z}A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
明文
V W X Y Z A B C D E F G H I J K L M N O P Q R S T U}V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
你的任务是对给定的密文进行解密得到明文。
你需要注意的是，密文中出现的字母都是大写字母。密文中也包括非字母的字符，对这些字符不用进行解码。

### Input 
一行，给出密文，密文不为空，而且其中的字符数不超过200。

### Output
输出一行，即密文对应的明文。

###  Sample Input
```
NS BFW, JAJSYX TK NRUTWYFSHJ FWJ YMJ WJXZQY TK YWNANFQ HFZXJX
```
### Sample Output
```
IN WAR, EVENTS OF IMPORTANCE ARE THE RESULT OF TRIVIAL CAUSES
```

### Idea
简单利用转换关系式进行密文和明文转换。
规律:字母X对应的明文是``'A'+ (21+X-'A')%26``

###  Codes
```cpp
#include<iostream>
#include<cstring> 
using namespace std;
int main(){
	string str;int s=0;
	getline(cin,str);
	int len=str.length();
	for(int i=0;i<len;++i)
	{
	 if('A'<=str[i] && str[i]<='Z'){
	  s=str[i]-'A';
	  str[i]='A'+(21+s)%26;	
	 } 
	}
	cout<<str<<endl;
	return 0;
}
```

## Problem D- Sushi for Two
### Description
Arkady invited Anna for a dinner to a sushi restaurant. The restaurant is a bit unusual: it offers nn pieces of sushi aligned in a row, and a customer has to choose a continuous subsegment of these sushi to buy.

The pieces of sushi are of two types: either with tuna or with eel. Let's denote the type of the ii-th from the left sushi as titi, where ti=1ti=1 means it is with tuna, and ti=2ti=2 means it is with eel.

Arkady does not like tuna, Anna does not like eel. Arkady wants to choose such a continuous subsegment of sushi that it has equal number of sushi of each type and each half of the subsegment has only sushi of one type. For example, subsegment [2,2,2,1,1,1][2,2,2,1,1,1] is valid, but subsegment [1,2,1,2,1,2][1,2,1,2,1,2] is not, because both halves contain both types of sushi.

Find the length of the longest continuous subsegment of sushi Arkady can buy.
### Input 
The first line contains a single integer nn (2≤n≤1000002≤n≤100000) — the number of pieces of sushi.

The second line contains nn integers t1t1, t2t2, ..., tntn (ti=1ti=1, denoting a sushi with tuna or ti=2ti=2, denoting a sushi with eel), representing the types of sushi from left to right.

It is guaranteed that there is at least one piece of sushi of each type. Note that it means that there is at least one valid continuous segment.

### Output
Print a single integer — the maximum length of a valid continuous segment.

### Sample Input
```
7
2 2 2 1 1 2 2
```
### Sample Output
```
4
```
### Idea
这道题可以分几步，先实现把相同的连续字符作为一段，把每段起点记录下来形成列表。
然后通过后段的起点-前一段的起点得到每段的长度。(最后一段由n+1-最后一段起点得到)
对于一个合法序列，必然是由两个不同段组成的，而上面得到的段，相邻之间必然是不同段，所以我们只需要考虑相邻的两段，
由于需要长度相等，所以相邻两段较短的一段作为标准，两段取同一长度组成序列，只需要遍历一遍找到最大值即可。属于O(N)复杂度

### Codes
```cpp
#include<iostream> 
#include<cmath>
using namespace std;
const int maxn=100005;
int n,s[maxn];
int t[maxn],f[maxn];
void solve(){
	s[0]=0; int tot=0,ans=0; 
	for(int i=1;i<=n;++i){
		if(s[i]!=s[i-1]) t[++tot]=i;  
	}
	t[++tot]=n+1; int len;
	for(int i=1;i<tot;++i) f[i]=t[i+1]-t[i];  
	for(int i=1;i<tot-1;++i){
		len=min(f[i],f[i+1]);
		if(ans<len) ans=len;
	} 
	printf("%d",ans*2);
}
int main(){
	scanf("%d",&n);
	for(int i=1;i<=n;++i) {
	  scanf("%d",&s[i]);	 
	}
	solve();
	return 0;
}
```

## Problem E-Cash Machine
### Description
A Bank plans to install a machine for cash withdrawal. The machine is able to deliver appropriate @ bills for a requested cash amount. The machine uses exactly N distinct bill denominations, say Dk, k=1,N, and for each denomination Dk the machine has a supply of nk bills. For example,

N=3, n1=10, D1=100, n2=4, D2=50, n3=5, D3=10

means the machine has a supply of 10 bills of @100 each, 4 bills of @50 each, and 5 bills of @10 each.

Call cash the requested amount of cash the machine should deliver and write a program that computes the maximum amount of cash less than or equal to cash that can be effectively delivered according to the available bill supply of the machine.
### Input
The program input is from standard input. Each data set in the input stands for a particular transaction and has the format:

cash N n1 D1 n2 D2 ... nN DN

where 0 <= cash <= 100000 is the amount of cash requested, 0 <=N <= 10 is the number of bill denominations and 0 <= nk <= 1000 is the number of available bills for the Dk denomination, 1 <= Dk <= 1000, k=1,N. White spaces can occur freely between the numbers in the input. The input data are correct.

### Output
For each set of data the program prints the result to the standard output on a separate line as shown in the examples below.

### Sample Input
```
735 3  4 125  6 5  3 350
633 4  500 30  6 100  1 5  0 1
735 0
0 3  10 100  10 50  10 10
```
### Sample Output
```
735
630
0
0
```
### Idea
这道题属于刚学的多重背包问题，有n种面额钱币，每种有C[i]件，每种的价值W[i]就是其面额大小，背包容量是给定需要兑换的现金数Sum。
先对每种钱币进行二进制拆分，比如4张125的可以拆分为125,250,125。
之后进行0-1背包。由于本题不需要打印方案，所以我们选择滚动数组进行递推。把f[i][j] 由 f[i-1][j] 和 f[i-1][j-w[i]] 两个子问题递推过来。

### Codes
```cpp
#include<iostream> 
#include<cstring>
using namespace std;
const int maxn=1010;
const int MAXN=1e5;
int N,Sum,cnt;
int W[maxn], C[maxn];//面额,数量 
int ww[MAXN],f[MAXN];
void Part(){
	cnt=0;
	for(int i=1;i<=N;++i){
		int t=C[i];
		for(int k=1;k<=t;k<<=1){
			cnt++;
			ww[cnt]=k*W[i]; 
			t-=k;
		}
		if(t>0){
			cnt++;
			ww[cnt]=t*W[i]; 
		}
	}
}
void solve(){
	if(N==0||Sum==0) { printf("0\n"); return; } 
	Part(); 
	memset(f,0,sizeof(f));
	for(int i=1;i<=cnt;++i)
		for(int j=Sum;j>=ww[i];--j){
			f[j]=max(f[j],f[j-ww[i]]+ww[i]);
		}
	int ans=f[Sum];
	printf("%d\n",ans);
}
int main(){
	while(~scanf("%d%d",&Sum,&N)){
		for(int i=1;i<=N;++i){
			scanf("%d%d",&C[i],&W[i]);
		} 
		solve();
	}
	return 0;
}
```

## Problem F- CD
### Description
You have a long drive by car ahead. You have a tape recorder, but unfortunately your best music is on CDs. You need to have it on tapes so the problem to solve is: you have a tape N minutes long. How to choose tracks from CD to get most out of tape space and have as short unused space as possible.

Assumptions:
```
• number of tracks on the CD does not exceed 20
• no track is longer than N minutes
• tracks do not repeat
• length of each track is expressed as an integer number
• N is also integer
```
Program should find the set of tracks which fills the tape best and print it in the same sequence as the tracks are stored on the CD

### Input
Any number of lines. Each one contains value N, (after space) number of tracks and durations of the tracks. For example from first line in sample data: N = 5, number of tracks=3, first track lasts for 1 minute, second one 3 minutes, next one 4 minutes
### Output
Set of tracks (and durations) which are the correct solutions and string ‘sum:’ and sum of duration times.

### Sample Input
```
5 3 1 3 4
10 4 9 8 4 2
20 4 10 5 7 4
90 8 10 23 1 2 3 4 5 7
45 8 4 10 44 43 12 9 8 2
```
### Sample Output
```
1 4 sum:5
8 2 sum:10
10 5 4 sum:19
10 23 1 2 3 4 5 7 sum:55
4 10 12 9 8 2 sum:45
```
### Idea
这道题就是0-1背包问题了。背包容量是总时间，物品N件是CD数量。每件CD的时间是物品价值。
第 i件物品由“前i-1件物品放入容量为j的背包中”和“前i-1件物品放入容量为j-W[i]的背包之间的价值较大的作为策略。
中”,f[i][j]=max(f[i][j],f[i-1][j-W[i]]+W[i])
另外我们需要顺序给出方案，所以需要倒回去遍历一遍f[i][N]的情况，并把选择了的给打印出来，这里我把数字转化成string类型最后放在一起打印。

### Codes
```cpp
#include<iostream> 
#include<cstdio>
#include<cmath> 
#include<cstring>
using namespace std; 
const int maxn=10005;
int N,M;string ans;
int W[22];
int f[maxn][maxn];
void solve(){
	for(int i=0;i<=N;++i)
		f[0][i]=0;
	for(int i=1;i<=M;++i)
		for(int j=0;j<=N;++j){
			f[i][j]=f[i-1][j];
			if(j-W[i]>=0)
				f[i][j]=max(f[i][j],f[i-1][j-W[i]]+W[i]);
		}
	string str;
	str=to_string(f[M][N]); 
	ans="sum:"+str;
	for(int i=M;i>1;--i){ 
		if(f[i][N]!=f[i-1][N]){
			str=to_string(W[i]);
			ans=str+" "+ans;
			N-=W[i];
		}
	} 
	if(f[1][N]>0){
	str=to_string(W[1]);
	ans=str+" "+ans;	
	} 
	printf("%s\n",ans.c_str());
}
int main(){
	while(~scanf("%d",&N)){
		scanf("%d",&M);
		for(int i=1;i<=M;++i)
			scanf("%d",&W[i]);
		solve();
	}
}
```

#  结束！  [返回首页](./index.md) [下篇月测三](./CSP-M3.md)
