#  程序设计思维与实践 月测三
## Problem A-瑞神的序列
### Description
瑞神的数学一向是最好的，连强大的咕咕东都要拜倒在瑞神的数学水平之下，虽然咕咕东很苦
恼，但是咕咕东拿瑞神一点办法都没有。
5.1期间大家都出去玩了，只有瑞神还在孜孜不倦的学习，瑞神想到了一个序列，这个序列长度为
，也就是一共有 个数，瑞神给自己出了一个问题：数列有几段？
段的定义是连续的相同的最长整数序列
### Input
输入第一行一个整数n，表示数的个数
接下来一行n个空格隔开的整数，表示不同的数字
### Output
输出一行，这个序列有多少段
### Sample Input
```
12
2 3 3 6 6 6 1 1 4 5 1 4
```
### Sample Output
```
8
```
### Idea
遇到与前一位字符不一样，段数就要加一
### Codes
```
#include<iostream>
#include<cstdio>
using namespace std;
int n,tot;
int main(){
	tot=0;
	scanf("%d",&n);
	int a,b;
	scanf("%d",&a);tot=1;
	for(int i=1;i<n;++i){
	  scanf("%d",&b);
	  if(a!=b) ++tot;
	  a=b;
	}
	printf("%d",tot);
	return 0;
} 
```

## Problem B- 消消乐大师
### Description
Q老师是个很老实的老师，最近在积极准备考研。Q老师平时只喜欢用Linux系统，所以Q老师的电
脑上没什么娱乐的游戏，所以Q老师平时除了玩Linux上的赛车游戏SuperTuxKart之外，就是喜欢
消消乐了。
游戏在一个包含有n 行m 列的棋盘上进行，棋盘的每个格子都有一种颜色的棋子。当一行或一列
上有连续三个或更多的相同颜色的棋子时，这些棋子都被消除。当有多处可以被消除时，这些地
方的棋子将同时被消除。
一个棋子可能在某一行和某一列同时被消除。
由于这个游戏是闯关制，而且有时间限制，当Q老师打开下一关时，Q老师的好哥们叫Q老师去爬
泰山去了，Q老师不想输在这一关，所以它来求助你了！！
### Input
输入第一行包含两个整数n,m，表示行数和列数
接下来n行m列，每行中数字用空格隔开，每个数字代表这个位置的棋子的颜色。数字都大于0.
### Output
输出n行m列，每行中数字用空格隔开，输出消除之后的棋盘。（如果一个方格中的棋子被消除，
则对应的方格输出0，否则输出棋子的颜色编号。）
### Sample Input1
```
4 5
2 2 3 1 2
3 4 5 1 4
2 3 2 1 3
2 2 2 4 4
```
### Sample Output1
```
2 2 3 0 2
3 4 5 0 4
2 3 2 0 3
0 0 0 4 4
```
### Sample Input2
```
4 5
2 2 3 1 2
3 1 1 1 1
2 3 2 1 3
2 2 3 3 3
```
### Sample Output2
```
2 2 3 0 2
3 0 0 0 0
2 3 2 0 3
2 2 0 0 0
```
### Idea
横向遍历一遍，纵向遍历一遍，每次遇到重复出现>2个的字符段就都标记一下，show[][]是用来标记是否打印0的。
### Codes
```
#include<iostream>
#include<cstdio>
using namespace std;
int n,m;
int Map[30][30];
bool show[30][30];
bool checkRow(int i,int j){ 
	if(Map[i][j-2]==Map[i][j-1]  &&  Map[i][j-1]==Map[i][j]){
	show[i][j-2]=show[i][j-1]=show[i][j]=false; return true;	
	}
	else return false;
}
bool checkCol(int i,int j){
	if(Map[i-2][j]==Map[i-1][j]  &&  Map[i-1][j]==Map[i][j]){
	show[i-2][j]=show[i-1][j]=show[i][j]=false; return true;	
	}
	else return false;
}
void visRow(int i){//第i行 
	int cnt,j=2;
	while(j<m){
		if(checkRow(i,j)){
		  cnt=Map[i][j];
		  while(j<m){
			if(Map[i][j]!=cnt) break;
			else { show[i][j]=false;	++j; }
		  }	
		  j+=2;continue;
		}
		else ++j;
	}
}
void visCol(int j){//第j列 
    int cnt,i=2;
	while(i<n){
		if(checkCol(i,j)){
		  cnt=Map[i][j];
		  while(i<n){
			if(Map[i][j]!=cnt) break;
			else { show[i][j]=false;	++i; }
		  }	
		  i+=2;continue;
		}
		else ++i;
	}
}
void solve(){
	for(int i=0;i<n;++i) visRow(i); 
	for(int j=0;j<m;++j) visCol(j); 
	for(int i=0;i<n;++i){ 
		for(int j=0;j<m;++j){
	        if(show[i][j])
			  printf("%d",Map[i][j]); 
			else printf("0");
			if(j!=m-1) printf(" ");
		}
		if(i!=n-1)printf("\n");
	}
}
int main(){
	scanf("%d%d",&n,&m);
	for(int i=0;i<n;++i){
	  for(int j=0;j<m;++j){
		scanf("%d",&Map[i][j]);	
		show[i][j]=true;
	  }
	}
	solve();
	return 0;
}
```

## Problem C-咕咕东学英语
### Description
咕咕东很聪明，但他最近不幸被来自宇宙的宇宙射线击中，遭到了降智打击，他的英语水平被归
零了！这一切的始作俑者宇宙狗却毫不知情！
此时咕咕东碰到了一个好心人——TT，TT在吸猫之余教咕咕东学英语。今天TT打算教咕咕东字母A
和字母B，TT给了咕咕东一个只有大写A、B组成的序列，让咕咕东分辨这些字母。
但是咕咕东的其他学科水平都还在，敏锐的咕咕东想出一个问题考考TT：咕咕东问TT这个字符串
有多少个子串是Delicious的。
TT虽然会做这个问题，但是他吸完猫发现辉夜大小姐更新了，不想回答这个问题，并抛给了你，
你能帮他解决这个问题吗？
Delicious定义：对于一个字符串，我们认为它是Delicious的当且仅当它的每一个字符都属于一个
大于1的回文子串中。

### Input
输入第一行一个正整数n，表示字符串长度
接下来一行，一个长度为n只由大写字母A、B构成的字符串。
### Output
输出仅一行，表示符合题目要求的子串的个数。
### Sample Input
```
5
AABBB
```

### Sample Output
```
6
```

### Idea
[](https://www.xupengbo.cn/wp-content/uploads/2020/05/ABstring.bmp)

### Codes
```
#include<iostream>
#include<cstdio>
#define ll long long
using namespace std;
const ll maxn=300005;
ll n,ans;
char str[maxn];ll t[maxn];
void solve(){ 
	ll tot=0;t[0]=0;
 	for(ll i=1;i<n;++i){
		if(str[i]!=str[i-1]) t[++tot]=i;  
	}
	t[++tot]=n; ans=(n-1)*n/2; 
	ans-=(t[tot]+t[tot-1]-t[1]-t[0]);
	ans+=(tot-1); printf("%lld",ans);
}
int main(){
	scanf("%lld",&n); scanf("%s",str); 
	solve();
	return 0;
}
```
