#  程序设计思维与实践第十一周  [返回首页](./index.md) [上篇week10作业+限时模拟](./week10.md)
## Problem A-买房子
### Description 
蒜头君从现在开始工作，年薪 NN 万。他希望在蒜厂附近买一套 6060 平米的房子，现在价格是 200200 万。假设房子价格以每年百分之 KK 增长，并且蒜头君未来年薪不变，且不吃不喝，不用交税，每年所得 NN 万全都积攒起来，问第几年能够买下这套房子？（第一年年薪 NN 万，房价 200200 万）
 
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
不旋转:A[i][j]=B[i][j]
旋转90度:A[i][j]=B[j][N-1-i]
旋转180度:A[i][j]=B[N-1-i][N-1-j]
旋转270度:A[i][j]=B[N-1-j][i]

### Codes
```
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
```
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

### Input

### Output

### Sample Input
```

```
### Sample Output
```

```
### Idea

### Codes
```

```

## Problem E-Cash Machine
### Description

### Input

### Output

### Sample Input
```

```
### Sample Output
```

```
### Idea

### Codes
```

```

## Problem F- CD
### Description

### Input

### Output

### Sample Input
```

```
### Sample Output
```

```
### Idea

### Codes
```

```

#  结束！  [返回首页](./index.md) [下篇待定]
