#  程序设计思维与实践第十一周  [返回首页](./index.md) [上篇week10作业+限时模拟](./week10.md)
## Problem A-买房子
### Description 
<p>蒜头君从现在开始工作，年薪&nbsp;N<em>N</em>&nbsp;万。他希望在蒜厂附近买一套&nbsp;6060&nbsp;平米的房子，现在价格是&nbsp;200200&nbsp;万。假设房子价格以每年百分之&nbsp;K<em>K</em>&nbsp;增长，并且蒜头君未来年薪不变，且不吃不喝，不用交税，每年所得&nbsp;N<em>N</em>&nbsp;万全都积攒起来，问第几年能够买下这套房子？（第一年年薪&nbsp;N<em>N</em>&nbsp;万，房价&nbsp;200200&nbsp;万）</p>
 
### Input  
 
<p>一行，包含两个正整数&nbsp;N(10 \le N \le 50)<em>N</em>(10≤<em>N</em>≤50)，K(1 \le K \le 20)<em>K</em>(1≤<em>K</em>≤20)，中间用单个空格隔开。</p>
 
 
### Output 

<p>如果在第&nbsp;2020&nbsp;年或者之前就能买下这套房子，则输出一个整数&nbsp;M<em>M</em>，表示最早需要在第&nbsp;M<em>M</em>&nbsp;年能买下；否则输出<code>"Impossible"</code>。</p>

<p>输出时每行末尾的多余空格，不影响答案正确性</p>

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

不需要旋转则输出 00
``
顺时针旋转 90° 则输出 11
顺时针旋转 180° 则输出 22
顺时针旋转 270° 则输出 33
若不满足以上四种情况则输出 -1−1
若满足多种情况，则输出较小的数字
``
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
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio>
using namespace std;
int A[21][21],B[21][21];
int N;
void solve(){
	bool f0=true,f1=true,f2=true,f3=true;
	for(int i=0;i&lt;N;++i) 
	  for(int j=0;j&lt;N;++j)
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
	scanf("%d",&amp;N);
	for(int i=0;i&lt;N;++i) 
	  for(int j=0;j&lt;N;++j)
	    scanf("%d",&amp;A[i][j]);
	for(int i=0;i&lt;N;++i) 
	  for(int j=0;j&lt;N;++j)
	    scanf("%d",&amp;B[i][j]);
	solve();
} </code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem C-简单密码</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Julius&nbsp;Caesar&nbsp;曾经使用过一种很简单的密码。对于明文中的每个字符，将它用它字母表中后&nbsp;55&nbsp;位对应的字符来代替，这样就得到了密文。比如字符<code>'A'</code>用<code>'F'</code>来代替。如下是密文和明文中字符的对应关系。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>密文\text{A B C D E F G H I J K L M N O P Q R S T U V W X Y Z}A&nbsp;B&nbsp;C&nbsp;D&nbsp;E&nbsp;F&nbsp;G&nbsp;H&nbsp;I&nbsp;J&nbsp;K&nbsp;L&nbsp;M&nbsp;N&nbsp;O&nbsp;P&nbsp;Q&nbsp;R&nbsp;S&nbsp;T&nbsp;U&nbsp;V&nbsp;W&nbsp;X&nbsp;Y&nbsp;Z</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>明文\text{V W X Y Z A B C D E F G H I J K L M N O P Q R S T U}V&nbsp;W&nbsp;X&nbsp;Y&nbsp;Z&nbsp;A&nbsp;B&nbsp;C&nbsp;D&nbsp;E&nbsp;F&nbsp;G&nbsp;H&nbsp;I&nbsp;J&nbsp;K&nbsp;L&nbsp;M&nbsp;N&nbsp;O&nbsp;P&nbsp;Q&nbsp;R&nbsp;S&nbsp;T&nbsp;U</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>你的任务是对给定的密文进行解密得到明文。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>你需要注意的是，密文中出现的字母都是大写字母。密文中也包括非字母的字符，对这些字符不用进行解码。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

一行，给出密文，密文不为空，而且其中的字符数不超过&nbsp;200200。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出一行，即密文对应的明文。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>NS BFW, JAJSYX TK NRUTWYFSHJ FWJ YMJ WJXZQY TK YWNANFQ HFZXJX</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>IN WAR, EVENTS OF IMPORTANCE ARE THE RESULT OF TRIVIAL CAUSES</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstring> 
using namespace std;
int main(){
	string str;int s=0;
	getline(cin,str);
	int len=str.length();
	for(int i=0;i&lt;len;++i)
	{
	 if('A'&lt;=str[i] &amp;&amp; str[i]&lt;='Z'){
	  s=str[i]-'A';
	  str[i]='A'+(21+s)%26;	
	 } 
	}
	cout&lt;&lt;str&lt;&lt;endl;
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem D- Sushi for Two </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>东东和他的女朋友(幻想的)去寿司店吃晚餐(在梦中)，他发现了一个有趣的事情，这家餐厅提供的 n 个的寿司被连续的放置在桌子上 (有序)，东东可以选择一段连续的寿司来吃</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>东东想吃鳗鱼，但是东妹想吃金枪鱼。核 平 起 见，他们想选择一段连续的寿司（这段寿司必须满足金枪鱼的数量等于鳗鱼的数量，且前一半全是一种，后一半全是另外一种）我们用1代表鳗鱼，2代表金枪鱼。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>比如，[2,2,2,1,1,1]这段序列是合法的，[1,2,1,2,1,2]是非法的。因为它不满足第二个要求。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>东东希望你能帮助他找到最长的一段合法寿司，以便自己能吃饱。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输入：<br>第一行：一个整数n（2≤n≤100000），寿司序列的长度。<br>第二行：n个整数（每个整数不是1就是2，意义如上所述）

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出：一个整数（代表东东可以选择的最长的一段连续的且合法的寿司）

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>7
2 2 2 1 1 2 2</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream> 
#include&lt;cmath>
using namespace std;
const int maxn=100005;
int n,s[maxn];
int t[maxn],f[maxn];
void solve(){
	s[0]=0; int tot=0,ans=0; 
	for(int i=1;i&lt;=n;++i){
		if(s[i]!=s[i-1]) t[++tot]=i;  
	}
	t[++tot]=n+1; int len;
	for(int i=1;i&lt;tot;++i) f[i]=t[i+1]-t[i];  
	for(int i=1;i&lt;tot-1;++i){
		len=min(f[i],f[i+1]);
		if(ans&lt;len) ans=len;
	} 
	printf("%d",ans*2);
}
int main(){
	scanf("%d",&amp;n);
	for(int i=1;i&lt;=n;++i) {
	  scanf("%d",&amp;s[i]);	 
	}
	solve();
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem E- <strong style="user-select: auto;">Cash Machine</strong> </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

A Bank plans to install a machine for cash withdrawal. The machine is able to deliver appropriate @ bills for a requested cash amount. The machine uses exactly N distinct bill denominations, say Dk, k=1,N, and for each denomination Dk the machine has a supply of nk bills. For example,</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>N=3, n1=10, D1=100, n2=4, D2=50, n3=5, D3=10</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>means the machine has a supply of 10 bills of @100 each, 4 bills of @50 each, and 5 bills of @10 each.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Call cash the requested amount of cash the machine should deliver and write a program that computes the maximum amount of cash less than or equal to cash that can be effectively delivered according to the available bill supply of the machine.

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

The program input is from standard input. Each data set in the input stands for a particular transaction and has the format:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>cash N n1 D1 n2 D2 ... nN DN</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>where 0 &lt;= cash &lt;= 100000 is the amount of cash requested, 0 &lt;=N &lt;= 10 is the number of bill denominations and 0 &lt;= nk &lt;= 1000 is the number of available bills for the Dk denomination, 1 &lt;= Dk &lt;= 1000, k=1,N. White spaces can occur freely between the numbers in the input. The input data are correct.

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>For each set of data the program prints the result to the standard output on a separate line as shown in the examples below. </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>735 3  4 125  6 5  3 350
633 4  500 30  6 100  1 5  0 1
735 0
0 3  10 100  10 50  10 10</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>735
630
0
0</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream> 
#include&lt;cstring>
using namespace std;
const int maxn=1010;
const int MAXN=1e5;
int N,Sum,cnt;
int W[maxn], C[maxn];//面额,数量 
int ww[MAXN],f[MAXN];
void Part(){
	cnt=0;
	for(int i=1;i&lt;=N;++i){
		int t=C[i];
		for(int k=1;k&lt;=t;k&lt;&lt;=1){
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
	//for(int i=1;i&lt;=cnt;i++)  	cout&lt;&lt;ww[i]&lt;&lt;" "; cout&lt;&lt;endl;
	memset(f,0,sizeof(f));
	for(int i=1;i&lt;=cnt;++i)
		for(int j=Sum;j>=ww[i];--j){
			f[j]=max(f[j],f[j-ww[i]]+ww[i]);
		}
	int ans=f[Sum];
	printf("%d\n",ans);
}
int main(){
	while(~scanf("%d%d",&amp;Sum,&amp;N)){
		for(int i=1;i&lt;=N;++i){
			scanf("%d%d",&amp;C[i],&amp;W[i]);
		} 
		solve();
	}
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem F- CD </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> You have a long drive by car ahead. You have a tape recorder, but unfortunately your best music is on CDs. You need to have it on tapes so the problem to solve is: you have a tape N minutes long. How to choose tracks from CD to get most out of tape space and have as short unused space as possible.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> Assumptions:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> • number of tracks on the CD does not exceed 20</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> • no track is longer than N minutes </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>• tracks do not repeat </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>• length of each track is expressed as an integer number</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> • N is also integer </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>  Program should find the set of tracks which fills the tape best and print it in the same sequence as the tracks are stored on the CD</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

Any number of lines. Each one contains value N, (after space) number of tracks and durations of the
tracks. For example from first line in sample data: N = 5, number of tracks=3, first track lasts for 1
minute, second one 3 minutes, next one 4 minutes

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

Set of tracks (and durations) which are the correct solutions and string ‘sum:’ and sum of duration
times.

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">5 3 1 3 4
10 4 9 8 4 2
20 4 10 5 7 4
90 8 10 23 1 2 3 4 5 7
45 8 4 10 44 43 12 9 8 2</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1 4 sum:5
8 2 sum:10
10 5 4 sum:19
10 23 1 2 3 4 5 7 sum:55
4 10 12 9 8 2 sum:45</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream> 
#include&lt;cstring>
using namespace std;
const int maxn=1010;
const int MAXN=1e5;
int N,Sum,cnt;
int W[maxn], C[maxn];//面额,数量 
int ww[MAXN],f[MAXN];
void Part(){
	cnt=0;
	for(int i=1;i&lt;=N;++i){
		int t=C[i];
		for(int k=1;k&lt;=t;k&lt;&lt;=1){
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
	//for(int i=1;i&lt;=cnt;i++)  	cout&lt;&lt;ww[i]&lt;&lt;" "; cout&lt;&lt;endl;
	memset(f,0,sizeof(f));
	for(int i=1;i&lt;=cnt;++i)
		for(int j=Sum;j>=ww[i];--j){
			f[j]=max(f[j],f[j-ww[i]]+ww[i]);
		}
	int ans=f[Sum];
	printf("%d\n",ans);
}
int main(){
	while(~scanf("%d%d",&amp;Sum,&amp;N)){
		for(int i=1;i&lt;=N;++i){
			scanf("%d%d",&amp;C[i],&amp;W[i]);
		} 
		solve();
	}
	return 0;
}</code></pre>
<!-- /wp:code -->
#  结束！  [返回首页](./index.md) [下篇待定]
