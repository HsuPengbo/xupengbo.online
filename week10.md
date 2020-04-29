#  程序设计思维与实践 week10 作业+限时模拟 &nbsp;[返回首页](./index.md)[上篇week9](./week9.md)
<!-- wp:heading -->
<h2>Problem A - 签到题</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong style="user-select: auto;">Time Limit:</strong>&nbsp;1000ms</td><td><strong style="user-select: auto;">Memory Limit:</strong>&nbsp;256MB</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3>Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>东东在玩游戏“Game23”。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>在一开始他有一个数字n，他的目标是把它转换成m，在每一步操作中，他可以将n乘以2或乘以3，他可以进行任意次操作。输出将n转换成m的操作次数，如果转换不了输出-1。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 输入的唯一一行包括两个整数n和m（1&lt;=n&lt;=m&lt;=5*10^8). </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出从n转换到m的操作次数，否则输出-1.

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"> 120 51840 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">7</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 2</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">42 42 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 2</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">0</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 3</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"> 48 72 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 3</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">-1
</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>这道题比较简单，直接算就是了，每次都可以选择*2或*3，当大于给定数时直接停止，不用更新标记值(初始为-1)，如果当等于给定数时，返回步骤数给标记值。最后打印即可。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
using namespace std;
long long n,m,num;
void getNum(long long x,int dp){
  if(x>m) return;
  if(x==m) {
  num=dp; return;
} 
  getNum(x*2,dp+1);
  getNum(x*3,dp+1);
}
int main()
{
    cin >> n >> m;
    num=-1;
    getNum(n,0);
    cout &lt;&lt; num;
    return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem B - LIS&amp;LCS</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong style="user-select: auto;">Time Limit:</strong>&nbsp;1000ms</td><td></td><td><strong style="user-select: auto;">Memory Limit:</strong>&nbsp;256MB</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3>Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>东东有两个序列A和B。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>他想要知道序列A的LIS和序列AB的LCS的长度。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>注意，LIS为严格递增的，即a1&lt;a2&lt;…&lt;ak(ai&lt;=1,000,000,000)。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 第一行两个数n，m（1&lt;=n&lt;=5,000,1&lt;=m&lt;=5,000）<br>第二行n个数，表示序列A<br>第三行m个数，表示序列B </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>  输出一行数据ans1和ans2，分别代表序列A的LIS和序列AB的LCS的长度 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">5 5
1 3 2 5 4
2 4 3 1 5 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">3 2 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>LIS：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>这里我用了贪心加二分法，用一个数组C,表示最后一个值为C[i]的子序列长度为i，C[1]=A[0],ans=1 然后从A[1]开始遍历，如果后面的数比ans大，说明以其为尾的子序列长度为ans+1，如果不是，则找到第一个比A[i]大的数C[pos]，置为A[i]，即如果A[i]为尾的话后面也许会生成更长的子序列的，最后看ans的值即可。ans就是答案.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>LCS：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>这里使用状态转移：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":320} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/04/image-8.png" alt="" class="wp-image-320"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
#define ll long long
const int maxn=5010;
int n,m;
long long A[maxn],B[maxn]; 
int C[maxn]; int dp[maxn][maxn];
void getLIS(){ 
    int ans=1, pos=0;C[1]=A[0];
  	for(int i=1;i&lt;n;++i){ 
  	if(A[i]>C[ans]) C[++ans]=A[i];
  	else {
  		pos=lower_bound(C,C+ans,A[i])-C;
		if(C[pos]>A[i])  C[pos]=A[i];
	  }
	}
	printf("%d",ans);
}
void getLCS(){
  for(int i=1;i&lt;=n;i++) {
    for(int j=1;j&lt;=m;j++) {
        if(A[i-1]==B[j-1]) dp[i][j]=dp[i-1][j-1]+1; 
        else dp[i][j]=max(dp[i-1][j],dp[i][j-1]); 
    }
  }
  printf("%d\n",dp[n][m]);
}
int main(){
	scanf("%d%d",&amp;n,&amp;m);
	for(int i=0;i&lt;n;++i)scanf("%lld",&amp;A[i]); 
	for(int i=0;i&lt;m;++i) scanf("%lld",&amp;B[i]);
	getLIS();  printf(" "); getLCS();
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem C - 拿数问题</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong style="user-select: auto;">Time Limit:</strong>&nbsp;1000MS</td><td><strong style="user-select: auto;">Memory Limit:</strong>&nbsp;256MB</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:paragraph -->
<p>Description</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

YJQ 上完第10周的程序设计思维与实践后，想到一个绝妙的主意，他对拿数问题做了一点小修改，使得这道题变成了 拿数问题 II。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>给一个序列，里边有 n 个数，每一步能拿走一个数，比如拿第 i 个数， Ai = x，得到相应的分数 x，但拿掉这个 Ai 后，x+1 和 x-1 (如果有 Aj = x+1 或 Aj = x-1 存在) 就会变得不可拿（但是有 Aj = x 的话可以继续拿这个 x）。求最大分数。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>本题和课上讲的有些许不一样，但是核心是一样，需要你自己思考。</strong></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行包含一个整数&nbsp;<em>n</em>&nbsp;(1 ≤ <em>n</em> ≤ 10<sup>5</sup>)，表示数字里的元素的个数</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>第二行包含n个整数<em>a</em><sub>1</sub>,&nbsp;<em>a</em><sub>2</sub>, ...,&nbsp;<em>a</em><sub><em>n</em></sub>&nbsp;(1 ≤ <em>a</em><sub><em>i</em></sub> ≤ 10<sup>5</sup>)</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>   输出一个整数：n(你能得到最大分值)。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Example</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">2<br>1 2</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">2</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">3<br>1 2 3</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">4</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">9<br>1 2 1 3 2 2 2 2 3</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">10 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>讲义中是不能拿相邻位置的数，这里是不能拿相邻大小的数。因为数的范围不是很大，所以就直接设一个数组num[]储存大小为i的数的数量，设状态数组dp[]。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>状态转移规则: dp[i] = max(dp[i-1] ,  dp[i-2]+ i的数量 * i )</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;cstdio>
#include&lt;algorithm>
#include&lt;cmath>
#define ll long long
using namespace std;
const int maxn=100005;
int n; ll ans; ll A[maxn],num[maxn]={0},dp[maxn]={0};
void solve(){
	sort(A,A+n);ans=-1;
	for(int i=A[0];i&lt;=A[n-1];++i){
	 dp[i]=max(dp[i-1],dp[i-2]+i*num[i]);
	 ans=max(ans,dp[i]);
	}
	printf("%lld\n",ans);
}
int main(){
	scanf("%d",&amp;n);
	for(int i=0;i&lt;n;++i){
		scanf("%lld",&amp;A[i]); ++num[A[i]];
	}
	solve();
	return 0;
} </code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem A - Divide a Cuboid</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong style="user-select: auto;">Time Limit:</strong>&nbsp;2000ms</td><td><strong style="user-select: auto;">Memory Limit:</strong>&nbsp;256MB</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3> Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We have a rectangular parallelepiped of size&nbsp;<em>A</em>×<em>B</em>×<em>C</em>, built with blocks of size&nbsp;1×1×1. Snuke will paint each of the&nbsp;<em>A</em>×<em>B</em>×<em>C</em>&nbsp;blocks either red or blue, so that:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>There is at least one red block and at least one blue block.</li><li>The union of all red blocks forms a rectangular parallelepiped.</li><li>The union of all blue blocks forms a rectangular parallelepiped.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Snuke wants to minimize the difference between the number of red blocks and the number of blue blocks. Find the minimum possible difference.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Constraints</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>2≤<em>A</em>,<em>B</em>,<em>C</em>≤10<sup>9</sup></li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The input is given from Standard Input in the following format:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><em>A</em> <em>B</em> <em>C</em>
</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Print the minimum possible difference between the number of red blocks and the number of blue blocks.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">3 3 3
</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 1</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">9
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>For example, Snuke can paint the blocks as shown in the diagram below. There are&nbsp;9&nbsp;red blocks and&nbsp;18&nbsp;blue blocks, thus the difference is&nbsp;9.</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://agc004.contest.atcoder.jp/img/agc/004/gatbantar/A_1.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 2</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">2 2 4
</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 2</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">0
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>For example, Snuke can paint the blocks as shown in the diagram below. There are&nbsp;8&nbsp;red blocks and&nbsp;8&nbsp;blue blocks, thus the difference is&nbsp;0.</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://agc004.contest.atcoder.jp/img/agc/004/gatbantar/A_2.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input 3</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">5 3 5
</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output 3</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">15
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>For example, Snuke can paint the blocks as shown in the diagram below. There are&nbsp;45&nbsp;red blocks and&nbsp;30&nbsp;blue blocks, thus the difference is&nbsp;9.</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://agc004.contest.atcoder.jp/img/agc/004/gatbantar/A_3.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>分析:对于一个确定的面来说要想使得这个长方块切开后，两部分体积差别最小，从这个面分的时候两部分的面积差值要最小，也就是尽量从中间切，如果偶数那就可以正好对半分，不是的话差值也就是1，再乘以对应截面面积就是差值体积。从长x宽 长x高 宽x高 三种面分别分开试试，最小的结果就是答案。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
using namespace std; 
#define LL long long
LL A,B,C;
void getAns(){ 
	LL ta=A%2,tb=B%2,tc=C%2;
	if(ta==0 || tb==0 || tc==0) {
		cout&lt;&lt;"0"; return;
	}
	LL ans1= B*C*ta;
	LL ans2= A*C*tb;
	LL ans3= A*B*tc; 
	if(ans1>ans2) ans1=ans2;
	if(ans1>ans3) ans1=ans3;
	cout&lt;&lt;ans1;
} 
int main(){
	cin >> A >> B >> C;
	getAns();
	return 0;
} </code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2> Problem B - Time Planner</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong>Time Limit:</strong>&nbsp;3000MS</td><td><strong>Memory Limit:</strong>&nbsp;30000K</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong style="user-select: auto;">Background</strong><br>Problems in computer science are often classified as belonging to a certain class of problems (e.g. NP, NP complete, unsolvable, . . . ). Whatever class of problems you have to solve in a team, there is always one main problem: To find a date where all the programmers can meet to work together on their project.<br><strong style="user-select: auto;">Problem</strong><br>Your task is to write a program that finds all possible appointments for a programming team that is busy all the time and therefore has problems in finding accurate dates and times for their meetings.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The first line of the input contains the number of scenarios.<br>For each scenario, you are first given the number m of team members in a single line, with 2 &lt;= m &lt;= 20.For every team member, there will be a line containing the number n of entries in this members calender (0 &lt;= n &lt;= 100), followed by n lines in the following format:<br></p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">YYYY MM DD hh mm ss YYYY MM DD hh mm ss some string here</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Each such line contains the year, month, day, hour, minute, and second of both starting and ending time for the appointment, and a string with the description of the appointment. All numbers are zero padded to match the given format, with single blanks in-between. The string at the end might contain blanks and is no longer than 100 characters. The dates are in the range January 1, 1800 midnight to January 1, 2200 midnight. For simplification, you may assume that all months (even February) have 30 days each, and no invalid dates (like January 31) will occur.<br>Note that the ending time of a team member's appointment specifies the point in time where this team member is ready to join a meeting.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The output for each scenario begins with a line containing Scenario #i:, where i is the number of the scenario starting at 1. Then print a line for each possible appointments that follows these rules:<br></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>at any time during the meeting, at least two team members need to be there<br></li><li>at any time during the meeting, at most one team member is allowed to be absent<br></li><li>the meeting should be at least one hour in length<br></li><li>all team members are willing to work 24 hours a day</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>For example, if there are three team members A, B and C, the following is a valid meeting: It begins solely with A and B. Later C joins the meeting and before the end, A may leave.<br>Always print the longest appointment possible satisfying these conditions, even if it is as long as 400 years. Sort these lines by date and time, and use the following format:<br>appointment possible from MM/DD/YYYY hh:mm:ss to MM/DD/YYYY hh:mm:ss<br>The numbers indicating month, day, year, hour, minute, and second should be zero padded in order to get the required number of characters. If no appointment is possible, just print a line containing no appointment possible Conclude the output for each scenario with a blank line.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">2
3
3
2002 06 28 15 00 00 2002 06 28 18 00 00 TUD Contest Practice Session
2002 06 29 10 00 00 2002 06 29 15 00 00 TUD Contest
2002 11 15 15 00 00 2002 11 17 23 00 00 NWERC Delft
4
2002 06 25 13 30 00 2002 06 25 15 30 00 FIFA World Cup Semifinal I
2002 06 26 13 30 00 2002 06 26 15 30 00 FIFA World Cup Semifinal II
2002 06 29 13 00 00 2002 06 29 15 00 00 FIFA World Cup Third Place
2002 06 30 13 00 00 2002 06 30 15 00 00 FIFA World Cup Final
1
2002 06 01 00 00 00 2002 06 29 18 00 00 Preparation of Problem Set
2
1
1800 01 01 00 00 00 2200 01 01 00 00 00 Solving Problem 8
0</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Scenario #1:
appointment possible from 01/01/1800 00:00:00 to 06/25/2002 13:30:00
appointment possible from 06/25/2002 15:30:00 to 06/26/2002 13:30:00
appointment possible from 06/26/2002 15:30:00 to 06/28/2002 15:00:00
appointment possible from 06/28/2002 18:00:00 to 06/29/2002 10:00:00
appointment possible from 06/29/2002 15:00:00 to 01/01/2200 00:00:00

Scenario #2:
no appointment possible</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>我的解题思路过程整体如下</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1.先实现字符与时间的互换：即实现从输入流接收的一行字符变成 long long型的数表示时间，再实现将数能够打印成给定格式。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2.分别表示出大家没有空的时间段数组，所有出现的时间点数组(利用vector可去重。然后都排好序。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>3.滑动遍历所有的点，先不断往右 checkL(L) 找到适合的时间段的起点L，然后从L+1不断往右找 checkR(R) ，直到找到不适合的终点R，前一位就是最适合的终点 R--;然后看这对起点和终点[L,R]是否>=1h,满足就按规定格式打印出来，并且给一个用来标记有没有合适时间段的值置为真。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>之后把L变为R+1,循环下去</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>结束时，如果这个标记最后为假就输出不存在的情况。 最后记得再空一行</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
#include&lt;cstdio>
#include&lt;cstring>
#include&lt;string>
#include&lt;vector>
#define ll long long
using namespace std; 
const int maxn=2010;
int T, m, n, Tot,Size;bool flag; ll B,E;//给定起终点  
struct TIME{
	ll L,R;
	bool operator&lt;(TIME p){
	  if(L!=p.L) return L&lt;p.L;
	  else return R&lt;p.R;
	}
}noMeets[maxn];	vector&lt;ll> Table;       //时间段, 时间点 
TIME create(ll l,ll r){
	TIME p;p.L=l;p.R=r; return p;
}
ll timetoll(ll Y,ll M,ll D,ll h,ll m,ll s){                   //时间转换成long long数 
    ll len=((Y-1800)*12 + M-1)*30+D-1;
	len=((len*24+h)*60+m)*60 + s; return len;
}
void lltotime(ll t){                                         //long long型数打印成格式时间 
    ll Y,M,D,h,m,s;
    s=t%60; t/=60;    m=t%60; t/=60;   h=t%24;t/=24;   D=t%30 +1;t/=30;   M=t%12+1;t/=12;   Y=t+1800;
	if(M&lt;10) { printf("0"); }  printf("%d/",M);  if(D&lt;10) { printf("0"); }  printf("%d/",D);
	printf("%d ",Y);                             if(h&lt;10) { printf("0"); }  printf("%d:",h);
	if(m&lt;10) { printf("0"); }  printf("%d:",m);  if(s&lt;10) { printf("0"); }  printf("%d",s);  
}
void init(){ //初始化 
	Size=0;Tot=0; flag=false;  Table.clear(); B= timetoll(1800,1,1,0,0,0); E= timetoll(2200,1,1,0,0,0); Table.push_back(B);Table.push_back(E);
}
void strtotime(string s){//字符转换成时间 
  	int len=s.size(); int TIM[12],t=-1,cnt=0;
  	for(int i=0;i&lt;len;++i){
  		if(s[i]&lt;'0'||s[i]>'9'){
  		 TIM[++t]=cnt;cnt=0;if(t==11) break;
		} else cnt=cnt*10 + (s[i]-'0');	 
	} 
	ll b=timetoll(TIM[0],TIM[1],TIM[2],TIM[3],TIM[4],TIM[5]),e=timetoll(TIM[6],TIM[7],TIM[8],TIM[9],TIM[10],TIM[11]);
	noMeets[Size++]=create(b,e); Table.push_back(b);Table.push_back(e);
}
bool checkL(int L){
	if(L>=Tot-1) return false;
	ll p=Table[L]; int cnt=0;
	for(int i=0;i&lt;Size;++i){
		if(noMeets[i].L&lt;=p){
			if(noMeets[i].R>p) ++cnt;
			else continue;
		}
		else break;
	}
	if(cnt&lt;2 &amp;&amp; (m-cnt)>1) return true;
	else return false;
}
bool checkR(int R){
	if(R>Tot-1) return false;
	ll p=Table[R]; int cnt=0;
	for(int i=0;i&lt;Size;++i){
		if(noMeets[i].L&lt;p){
			if(noMeets[i].R>=p) ++cnt;
			else continue;
		}
		else break;
	}
	if(cnt&lt;2 &amp;&amp; (m-cnt)>1) return true;
	else return false;	
}
bool checklen(ll p1,ll p2){
    if((p2-p1)>=3600 )return true;
	else return false;
}
void checkTIM(int L,int R){
	ll p1=Table[L],p2=Table[R];
	if(!checklen(p1,p2)) return;  flag=true;
	printf("appointment possible from "); lltotime(p1);
	printf(" to "); lltotime(p2); printf("\n");
}
void Solve(int t){
  //数据处理
  sort(Table.begin(),Table.end());sort(noMeets,noMeets + Size);
  Table.erase(unique(Table.begin(),Table.end()),Table.end());
  Tot=Table.size(); printf("Scenario #%d:\n",t);
  //从给定起点遍历所有出现的时间点 
  int L=0,R=0;
  while(L&lt;Tot &amp;&amp; R&lt;Tot){ 
    while(L&lt;Tot &amp;&amp; !checkL(L)) L++;	R=L+1;
	while(R&lt;Tot &amp;&amp; checkR(R))  R++;  R--;
	checkTIM(L,R); 	L=R+1;
  }
  if(!flag) printf("no appointment possible\n");
  printf("\n");
}
int main(){
	scanf("%d",&amp;T);string str;
	for(int i=1;i&lt;=T;++i){
	    scanf("%d",&amp;m);	init();
		for(int j=0;j&lt;m;++j){
			scanf("%d",&amp;n);cin.ignore();
			for(int k=0;k&lt;n;++k){
				getline(cin,str); strtotime(str);
			}
		}  Solve(i);
	}
	return 0;
} </code></pre>
<!-- /wp:code -->
# 结束！&nbsp;[返回首页](./index.md)[下篇待定]
