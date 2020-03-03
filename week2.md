# 程序设计思维与实践 习题 第二周
## Problem A- Maze
####  题目    
东东有一张地图，想通过地图找到妹纸。地图显示，0表示可以走，1表示不可以走，左上角是入口，右下角是妹纸，这两个位置保证为0。既然已经知道了地图，那么东东找到妹纸就不难了，请你编一个程序，写出东东找到妹纸的最短路线。

####  输入
输入是一个5 × 5的二维数组，仅由0、1两数字组成，表示法阵地图。
####  输出
输出若干行，表示从左上角到右下角的最短路径依次经过的坐标，格式如样例所示。数据保证有唯一解。
####  Sample Input
```
0 1 0 0 0
0 1 0 1 0
0 1 0 1 0
0 0 0 1 0
0 1 0 1 0
```
####  Sample Output
```
(0, 0)
(1, 0)
(2, 0)
(3, 0)
(3, 1)
(3, 2)
(2, 2)
(1, 2)
(0, 2)
(0, 3)
(0, 4)
(1, 4)
(2, 4)
(3, 4)
(4, 4)
```
####  思路
已知矩阵5*5的左上角(0,0)为出口，右下角(4,4)为出口。矩阵中(i,j)==0为路，(i,j)==1为障碍。需要找到最短路径并输出。
该题可采用 **BFS+队列** 来搜索**最短路径**，从入口开始将其插入队列，然后分别把其可达到的点依次插入队列(并将其(i,j)置为1保证不会再次进入队列)，直到达到出口。对于搜索中出现的点都保存他们的**父节点**的信息。最后再从**出口**根据其**父节点**信息**往回遍历**。
####  代码

```cpp
#include<iostream>
#include<queue>
#define _for(i,a,b) for(int i=(a);i<(b);i++)
using namespace std;
int Map[5][5];int Parent[5][5],Child[5][5];
int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
struct Node{
	int x, y;
};
queue<Node> Q; 
void VisitBFS(){
  int i=0,j=0,m,n; Parent[0][0]=0;
  Node p;   p.x=0; p.y=0;   Map[0][0]=1;
  Q.push(p); 
  while(Q.size()){
  	p=Q.front(); Q.pop();//取队首保存下来然后再出队
	i=p.x; j=p.y;
	if(i==4 && j==4) break;  //如果到达
  	_for(t,0,4)  //依次遍历上下左右四个点看是否满足可走，当然还要满足矩阵本身边界
  	{
  		m=i + dx[t]; n= j + dy[t];
  		if(Map[m][n]==0 && -1<m && m<5 &&-1< n && n<5){
  		  p.x=m;    p.y=n;
		  Q.push(p); Map[m][n]=1;  
		  Parent[m][n]=5*i+j;
		  }
	  } 
  }
}
void input(){ //输入
	_for(i,0,5)  _for(j,0,5) cin>>Map[i][j];
}
void output(){  //输出
 int i=4,j=4,m,n,P,C;
 while(!(i==0 && j==0)){  //根据把最短路径上的每个点的父节点换算成上一个点的子节点保存下来
 	P=Parent[i][j]; m=i;n=j;
	i=P/5;j=P%5; Child[i][j]=5*m+n;
 }cout<<"("<<i<<", "<<j<<")"<<endl; //先把起点输出
 while(true){ //从起点下一个点开始循环输出每个点
 	C=Child[i][j];i=C/5;j=C%5;
 	cout<<"("<<i<<", "<<j<<")";
	if(!(i==4 &&j==4)) cout<<endl;
	else break;
 }
}
int main(){
    input();
    VisitBFS();
	output();
	return 0;
}
```
## Problem B- Pour Water
####  题目  
倒水问题 "fill A" 表示倒满A杯，"empty A"表示倒空A杯，"pour A B" 表示把A的水倒到B杯并且把B杯倒满或A倒空。
####  输入
输入包含多组数据。每组数据输入 A, B, C 数据范围 0 < A <= B 、C <= B <=1000 、A和B互质。
####  输出
你的程序的输出将由一系列的指令组成。这些输出行将导致任何一个罐子正好包含C单位的水。每组数据的最后一行输出应该是“success”。输出行从第1列开始，不应该有空行或任何尾随空格。
####  Sample Input
```
2 7 5
2 7 4
```
####  Sample Output
```
fill B
pour B A
success
fill A
pour A B
fill A
pour A B
success
```
####  思路
A,B两个杯子，一 小一大。可以通过不断倒满A，将其倒入B中，即  A*(i++) \% B=C 初始 i=0，之后 i++。如果题目有解，必然能够找到有限  i  值。  \^_^ 不过当C较大且不是A的倍数时，很可能不是最优解
####  代码
```cpp
#include<iostream>
using namespace std;
int A,B,C;
const char str[7][10]={"fill A","fill B","empty A","empty B",
"pour A B","pour B A","success"};//有7种约定语句，但并不是都用到
void PourWater(int A,int B,int C){
  int i=0;int a=0,b=0,t=0;
  while((i*A)%B!=C){
  	cout<<str[0]<<endl;a=A;  	   //fill A
  	cout<<str[4]<<endl;t=b+A; b=(t>B)?B:t ; a=(t>B)?(t-B):0;  //pour A B,保证b都不会溢出
	if(b==C){ cout<<str[6]<<endl; return; }	
  	if(b==B){
  		 cout<<str[3]<<endl; b=0;  //empty B
  		 if(a>0)
  		 cout<<str[4]<<endl;b+=a;a=0;   //pour A B
  		 if(b==C)	break;
		   }  		   		 
	i++;
  } 
}
int main(){
	while(cin>>A>>B>>C){
		PourWater(A,B,C);
	}
	return 0;
}
```

## Problem A-化学 (编译器选 GNU G++)  
####  题目  
化学很神奇，以下是烷烃基。
![](https://github.com/HsuPengbo/HsuPengbo.github.io/blob/master/alkanyl000212.png)
假设如上图，这个烷烃基有6个原子和5个化学键，6个原子分别标号1~6，然后用一对数字 a,b 表示原子a和原子b间有一个化学键。这样通过5行a,b可以描述一个烷烃基

你的任务是甄别烷烃基的类别。

原子没有编号方法，比如 
<table>
	<tr> <td> A </td> <td> B </td> </tr>
	<tr> <td> 1-2 </td> <td> 1-3 </td> </tr>
	<tr> <td> 2-3 </td> <td> 2-3 </td> </tr>
	<tr> <td> 3-4 </td> <td> 2-4 </td> </tr>
	<tr> <td> 4-5 </td> <td> 4-5 </td> </tr>
	<tr> <td> 5-6 </td> <td> 5-6 </td> </tr>
</table>
A、B是同一种，本质上就是一条链，编号其实是没有关系的，可以在纸上画画就懂了
####  输入
输入第一行为数据的组数T（1≤T≤200000）。每组数据有5行，每行是两个整数a, b(1≤a,b≤6,a ≤b).数据保证，输入的烷烃基是以上5种之一
####  输出
每组数据，输出一行，代表烷烃基的英文名
####  Sample Input
```
2
1 2
2 3
3 4
4 5
5 6
1 4
2 3
3 4
4 5
5 6
```
####  Sample Output
```
n-hexane
3-methylpentane
```
####  思路
观察发现，
``n-hexane``有4个2*顶点；
``2,2-dimethylbutane`` 有1个2*顶点；
``2,3-dimethylbutane`` 有0个2*顶点；
但是``2-methylpentane``和 ``3-methylpentane`` 都有2个2*顶点；不过前者的两个2*顶点是直接连着的，但是后者的被3*顶点分开了。
据此我们可以把各种情况都分开。
####  代码
```cpp
#include<iostream>
#include<cstring>
using namespace std;
struct Point{
	int x;
	int y;
};
void Judge(Point *A,int num[]){
	int p=-1,q=-1; int t2=0;//2*顶点的数量 
	for(int i=1;i<7;i++){
      if(num[i]==2  ){
      	 t2++; if(p<0) p=i; else q=i;
	  } 
	}
	//t2=0,1,4都可直接判断出
	if(t2==4) { cout<<"n-hexane";return;	} 
	else if(t2==1) { cout<<"2,2-dimethylbutane";return;}
	else if(t2==0) { cout<<"2,3-dimethylbutane";return;	}
    else{ //第二种和第三种通过观察他们的两个2*顶点是否相连来区分
	  for(int i=0;i<5;i++)
	  {
	    if((A[i].x==p && A[i].y==q)||(A[i].x==q && A[i].y==p)){
	        cout<<"2-methylpentane";return;	}
	  }  
	  cout<<"3-methylpentane";return;	
	}
}
int main()
{
    int T;cin>>T; Point A[5];
	int a,b;int num[7];
	for(int i=0;i<T;i++) {
		memset(num,0,sizeof(num));
		for( int j=0;j<5;j++)
		{
			cin>>a>>b;
			A[j].x=a; A[j].y=b;
			num[a]++; num[b]++;
		}
		Judge(A,num);  cout<<endl;
	}
	return 0;
}
```
## Problem B-考试成绩+罚时的排名  
####  题目  
程序设计思维作业和实验使用的实时评测系统，具有及时获得成绩排名的特点，那它的功能是怎么实现的呢？
我们千辛万苦怼完了不忍直视的程序并提交以后，评测系统要么返回AC，要么是返回各种其他的错误，不论是怎样的错法，它总会给你记上一笔，表明你曾经在这儿被坑过，而当你历经千辛终将它AC之后，它便会和你算笔总账,表明这题共错误提交了几次。
    在岁月的长河中，你通过的题数虽然越来越多，但通过每题时你所共花去的时间（从最开始算起，直至通过题目时的这段时间）都会被记录下来，作为你曾经奋斗的痕迹。特别的，对于你通过的题目，你曾经的关于这题的每次错误提交都会被算上一定的单位时间罚时，这样一来，你在做出的题数上，可能领先别人很多，但是在做出同样题数的人中，你可能会因为罚时过高而处于排名上的劣势。例如某次考试一共八道题（A,B,C,D,E,F,G,H），每个人做的题都在对应的题号下有个数量标记，负数表示该学生在该题上有过的错误提交次数但到现在还没有AC，正数表示AC所耗的时间，如果正数a跟上了一对括号，里面有个正数b,则表示该学生AC了这道题，耗去了时间a，同时曾经错误提交了b次。例子可见下方的样例输入与输出部分。
 
####  输入
输入数据包含多行，第一行是共有的题数n（1≤n≤12）以及单位罚时m（10≤m≤20），之后的每行数据描述一个学生的信息，首先是学生的用户名（不多于10个字符的字串）其次是所有n道题的得分现状，其描述采用问题描述中的数量标记的格式，见上面的表格。
####  输出
根据这些学生的得分现状，输出一个实时排名。实时排名显然先按AC题数的多少排，多的在前，再按时间分的多少排，少的在前，如果凑巧前两者都相等，则按名字的字典序排，小的在前。每个学生占一行，输出名字（10个字符宽），做出的题数（2个字符宽，右对齐）和时间分（4个字符宽，右对齐）。名字、题数和时间分相互之间有一个空格。数据保证可按要求的输出格式进行输出。
####  Sample Input
```
8 20
GuGuDong  96     -3    40(3) 0    0    1      -8    0
hrz       107    67    -3    0    0    82     0     0
TT        120(3) 30    10(1) -3   0    47     21(2) -2
OMRailgun 0      -99   -8    0    -666 -10086 0     -9999996
yjq       -2     37(2) 13    -1   0    113(2) 79(1) -1
Zjm       0      0     57(5) 0    0    99(3)  -7    0
```
####  Sample Output
```
TT          5  348
yjq         4  342
GuGuDong    3  197
hrz         3  256
Zjm         2  316
OMRailgun   0    0
```
####  思路
1.  建立结构``student``把信息保存，信息包括``name``、作对数目``rNum``、总时间``time``
2. 接收每个人的``name`` 、每道题的相关信息，每个人总时间和作对数目的临时变量都初始化为0
   1.对于这些相关信息，每串字符串首为``'-'``或``'0'``时，说明没有作对，``rNum``不变，总时间不变
   2. 为正数，利用 `` A=A*10+s[i++] ``来增加总时间
   3. 遇到左括号说明存在罚时，需要再把罚时也加上去
3.  把所有人按照重定义后的比较法则，来进行排序

####  代码
```cpp
#include<iostream>
#include<cstdio>
#include<string>
#include<iomanip>
using namespace std;
struct student{
	string name;
	int rNum=0;
	int time=0;
	bool operator<(student b){ //重定义<
		if(rNum>b.rNum) return true;
		else if(rNum<b.rNum) return false;
		else{
			if(time<b.time) return true;
			else if(time>b.time) return false;
			else{
				if(name<b.name) return true;
				else return false;
			}
		}
	}
};
void ShellSort(student S[],int n){         //希尔排序，用其他排序方法也可以
    int i, j, cnt;
	student tmp; 
    for (cnt = n/ 2; cnt > 0; cnt /= 2) {    
        for (i = cnt; i < n; i++) {  
            tmp = S[i];  
            for (j = i - cnt; j >= 0 && tmp < S[j]; j -= cnt) {  
                S[j + cnt] = S[j];  
            }  
            S[j + cnt] = tmp;
        }  
    }
}
 int getrNum(string str){                  //如果是'-'或者'0'的话说明该题没有做对，返回0，否则返回1
 	if(str[0]=='-' ||str[0]=='0') return 0;
 	else return 1;
 }
int getTime(string str,int m){             //获取做题时间
	if(str[0]=='-') return 0;              //没有做对返回0
	int A=0,B=0;int s;
	bool punish=false; int Lb=0;           //罚时标记为假,当为真时才使用临时变量Lb
	int L=str.length();
	for(int i=0;i<L;i++){
		if(str[i]=='('){                   //遇到'('说明存在做错,罚时置为真
		  punish=true;Lb=i;                //保存罚时的字符首个位置
		  break;	
		} 
		 s=str[i]-'0';A=A*10+s;
	}
	if(punish==false)  { return A; } 
	else{                                  //有罚时就从Lb+1处开始计算罚时
		for(int i=Lb+1;i<L-1;i++){ 
			s=str[i]-'0';
			B=B*10+s;
		}
		A+=B*m;return A;
	}	
}
student S[1000];
int main(){
	int n,m,time,rNum, N=0;                //N用来保存人数
	string name,score;
	cin>>n>>m;
	while(cin>>name){
		time=0;rNum=0;                     //每次都把时间和作对数量置0
		for(int i=0;i<n;i++){
			cin>>score;
			rNum+=getrNum(score);          //作对数目
			time+=getTime(score,m);        //作对用时
		}
		S[N].name=name;  
		S[N].rNum=rNum;
		S[N++].time=time;                  //N++
	}
	ShellSort(S,N);                        //排序
	for(int i=0;i<N;i++){                  //输出时需要注意格式
		cout<<std::left<<setw(10)<<S[i].name<<" "<<std::right<<setw(2)<<S[i].rNum<<" "<<std::right<<setw(4)<<S[i].time<<endl;
	}
	return 0;
}
```
## Problem C-打牌 
####  题目  
瑞神HRZ因为疫情在家闲得无聊，同时他又非常厉害，所有的课对他来说都是水一水就能拿A+，所以他无聊，找来了另外三个人：咕咕东，腾神以及zjm来打牌（天下苦瑞神久矣）。
显然，牌局由四个人构成，围成一圈。我们称四个方向为北 东 南 西。对应的英文是North，East，South，West。游戏一共由一副扑克，也就是52张构成。开始，我们指定一位发牌员（东南西北中的一个，用英文首字母标识）开始发牌，发牌顺序为顺时针，发牌员第一个不发自己，而是发他的下一个人（顺时针的下一个人）。这样，每个人都会拿到13张牌。
现在我们定义牌的顺序，首先，花色是（梅花）<（方片）<（黑桃）<（红桃），（输入时，我们用C,D,S,H分别表示梅花，方片，黑桃，红桃，即其单词首字母）。对于牌面的值，我们规定2 < 3 < 4 < 5 < 6 < 7 < 8 < 9 < T < J < Q < K < A。
现在你作为上帝，你要从小到大排序每个人手中的牌，并按照给定格式输出。（具体格式见输出描述和样例输出）。
####  输入
 
输入包含多组数据
每组数据的第一行包含一个大写字符，表示发牌员是谁。如果该字符为‘#’则表示输入结束。
接下来有两行，每行有52个字符，表示了26张牌，两行加起来一共52张牌。每张牌都由两个字符组成，第一个字符表示花色，第二个字符表示数值。
 
####  输出
输出多组数据发牌的结果，每组数据之后需要额外多输出一个空行！！！！！
每组数据应该由24行的组成，输出按照顺时针方向，始终先输出South Player的结果，每位玩家先输出一行即玩家名称（东南西北），接下来五行，第一行和第五行输出固定格式（见样例），第二行和第四行按顺序和格式输出数值（见样例），第三行按顺序和格式输出花色（见样例）。
####  Sample Input
```
N
CTCAH8CJD4C6D9SQC7S5HAD2HJH9CKD3H6D6D7H3HQH4C5DKHKS9
SJDTS3S7S4C4CQHTSAH2D8DJSTSKS2H5D5DQDAH7C9S8C8S6C2C3
#
```
####  Sample Output
```
South player:
+---+---+---+---+---+---+---+---+---+---+---+---+---+
|6 6|A A|6 6|J J|5 5|6 6|7 7|9 9|4 4|5 5|7 7|9 9|T T|
| C | C | D | D | S | S | S | S | H | H | H | H | H |
|6 6|A A|6 6|J J|5 5|6 6|7 7|9 9|4 4|5 5|7 7|9 9|T T|
+---+---+---+---+---+---+---+---+---+---+---+---+---+
West player:
+---+---+---+---+---+---+---+---+---+---+---+---+---+
|2 2|5 5|9 9|K K|5 5|7 7|9 9|4 4|T T|J J|A A|8 8|A A|
| C | C | C | C | D | D | D | S | S | S | S | H | H |
|2 2|5 5|9 9|K K|5 5|7 7|9 9|4 4|T T|J J|A A|8 8|A A|
+---+---+---+---+---+---+---+---+---+---+---+---+---+
North player:
+---+---+---+---+---+---+---+---+---+---+---+---+---+
|3 3|4 4|J J|2 2|3 3|T T|Q Q|K K|8 8|Q Q|K K|2 2|3 3|
| C | C | C | D | D | D | D | D | S | S | S | H | H |
|3 3|4 4|J J|2 2|3 3|T T|Q Q|K K|8 8|Q Q|K K|2 2|3 3|
+---+---+---+---+---+---+---+---+---+---+---+---+---+
East player:
+---+---+---+---+---+---+---+---+---+---+---+---+---+
|7 7|8 8|T T|Q Q|4 4|8 8|A A|2 2|3 3|6 6|J J|Q Q|K K|
| C | C | C | C | D | D | D | S | S | H | H | H | H |
|7 7|8 8|T T|Q Q|4 4|8 8|A A|2 2|3 3|6 6|J J|Q Q|K K|
+---+---+---+---+---+---+---+---+---+---+---+---+---+
```
####  思路
这道题其实过程很简单，就是循环发牌+排序。只不过发牌的时候可以利用`` (i++)\%4``来保证在``0,1,2,3``之间循环。然后重定义<，再进行每个人的花色和牌面的排序。
####  代码
```cpp
#include<iostream>
#include<cstdio>
#include<string>
using namespace std;
const char Color[]={"CDSH"};                          //颜色序列
const char Spade[]={"23456789TJQKA"};                  //牌面序列
const char Peo[]={"SWNE"};                             //方向序列
const char Name[4][8]={"South","West","North","East"}; //名字
int Tran(const char *s,char c){                   //把字符换算成序列
	int i=0;
	while(i<13){
		if(s[i]==c) return i;
		else i++;
	}
}
struct Card{
	int color;                                    //颜色
	int spade;                                    //牌面
	bool operator<(Card b){                       //重定义
		if(color < b.color) return true;
		else if( color > b.color) return false;
		else{
			if(spade < b.spade) return true;
			else return false;
		}
	}
};
struct Plays{     
	Card cards[13];
}; 
Plays Player[4];                                    //S、W、N、E四个方向的人，每个人有13张牌

void ShellSort(Card *card){                         //排序
      int i, j, cnt,n=13;
	  Card tmp; 
      for (cnt = n/ 2; cnt > 0; cnt /= 2) {    
         for (i = cnt; i < n; i++) {  
            tmp = card[i];  
            for (j = i - cnt; j >= 0 && tmp < card[j]; j -= cnt) {  
                card[j + cnt] = card[j];  
            }  
            card[j + cnt] = tmp;
         }  
      }
}
void Output(){                                       //输出
	int t;
    	for(int i=0;i<4;i++){
    		cout<<Name[i]<<" player:"<<endl; 
    		cout<<"+---+---+---+---+---+---+---+---+---+---+---+---+---+"<<endl;
    		for(int j=0;j<13;j++){  t=Player[i].cards[j].spade;
			cout<<"|" << Spade[t]<<" "<< Spade[t]; } cout<<"|"<<endl;
    		for(int j=0;j<13;j++){ 	t=Player[i].cards[j].color;
			cout<<"|" << " "   << Color[t] << " ";  }     cout<<"|"<<endl;
    		for(int j=0;j<13;j++){  t=Player[i].cards[j].spade;
			cout<<"|" << Spade[t]<<" "<< Spade[t]; } cout<<"|"<<endl;
    		cout<<"+---+---+---+---+---+---+---+---+---+---+---+---+---+"<<endl;	
		}
}
void Input(int od){                                   //输入
	string str1,str2,str; char c,s;
	cin>>str1>>str2;
	str=str1+str2;                                    //把108个字符合一起 
	od++;                                             //从od方向的人开始发 
	int t;
	for(int i=0;i<13;i++) {
	  for(int j=0;j<4;j++){
		t=i*8+j*2;
    	c=Tran(Color,str[t]); s=Tran(Spade,str[t+1]); //每个人的牌都要把字符转换成数字信息
		Player[od%4].cards[i].color=c;
    	Player[od%4].cards[i].spade=s;
		od++;	 	                                  //od++%4就可以不断在这四个方向上循环
		}
	}
	for(int i=0;i<4;i++){                             //排序
		ShellSort(Player[i].cards);
	}
}
int main(){
    char X;int od; 
    while(cin>>X && X!='#'){
	    od=Tran(Peo,X);
    	Input(od);
    	Output();
    	cout<<endl;
	}
	return 0;
}
```
