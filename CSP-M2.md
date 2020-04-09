# 程序设计思维与实践 CSP-M2       &nbsp;    [返回首页](./index.md)&nbsp;  [上篇CSP-201604-4](./CSP01604-3.md)
## Problem  A- HRZ的序列  
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
### Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

相较于咕咕东，瑞神是个起早贪黑的好孩子，今天早上瑞神起得很早，刷B站时看到了一个序列 ，他对
这个序列产生了浓厚的兴趣，他好奇是否存在一个数 ，使得一些数加上 ，一些数减去 ，一些数不
变，使得整个序列中所有的数相等，其中对于序列中的每个位置上的数字，至多只能执行一次加运算或
减运算或是对该位置不进行任何操作。由于瑞神只会刷B站，所以他把这个问题交给了你！

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输入第一行是一个正整数 表示数据组数。 接下来对于每组数据，输入的第一个正整数 表示序列 的长
度，随后一行有 个整数，表示序列 。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出共包含 行，每组数据输出一行。对于每组数据，如果存在这样的K，输出"YES"，否则输出“NO”。
（输出不包含引号）

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Sample Input 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>2
5
1 2 3 4 5
5
1 2 3 4 5</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Sample Onput 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>NO
NO</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Note 
<!-- /wp:heading -->

<!-- wp:image {"id":187} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/04/捕获-2.png" alt="" class="wp-image-187"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
### Idea 
<!-- /wp:heading -->
   序列中一些数加上k ，一些减去k ，一些不变，最后序列中所有的数相等。也就是说这个序列最多存在三个离散的数值(a,b,c)。
  设a,b,c,d和a,b,c,d的bool标记.然后输入序列，先给a赋值,当存在序列值!=a且b的bool=false时,给b赋值，c,d同理。 
  最后只需要判断a,b,c,d的存在即可。d存在就NO,c存在时, a、b、c之间不存在一个数是另外两数的平均值时,也NO。其余情况都是YES。 

<!-- wp:heading {"level":3} -->
### Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio>
typedef  long long  ll;
using namespace std;
int t;int n;
ll a[10005];
ll x,y,z,p;
bool tx,ty,tz,tp;
bool check(ll b, ll c,ll d){
	ll sum= b+c+d;
	if(sum!=3*b &amp;&amp; sum!=3*c &amp;&amp; sum!=3*d) return false;
	else return true;
}
int main(){
	scanf("%d",&amp;t);ll sum;
	while(t--){
		scanf("%d",&amp;n);
		tx=ty=tz=tp=true;
		for(int i=0;i&lt;n;++i){
			scanf("%lld",&amp;a[i]);
			if(i==0 &amp;&amp; tx){
				x=y=z=p=a[i];tx=false;
			} 
			if(a[i]!=x&amp;&amp; ty){
			    y=a[i];ty=false;	
			} 
			if(a[i]!=x &amp;&amp;a[i]!=y &amp;&amp;tz){
				z=a[i];tz=false;
			}
			if(a[i]!=x&amp;&amp;a[i]!=y&amp;&amp;a[i]!=z &amp;&amp;tp){
				p=a[i];tp=false;
			}
		}
		sum=x+y+z;
		if(!tp) cout&lt;&lt;"NO"&lt;&lt;endl;
		else if(!tz &amp;&amp; !check(x,y,z)) cout&lt;&lt;"NO"&lt;&lt;endl;
		else cout&lt;&lt;"YES"&lt;&lt;endl;
	}
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
## Problem  B-HRZ学英语  
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
### Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 瑞神今年大三了，他在寒假学会了英文的26个字母，所以他很兴奋！于是他让他的朋友TT考考他，TT想 到了一个考瑞神的好问题：给定一个字符串，从里面寻找连续的26个大写字母并输出！但是转念一想， 这样太便宜瑞神了，所以他加大了难度：现在给定一个字符串，字符串中包括26个大写字母和特殊字 符'?'，特殊字符'？'可以代表任何一个大写字母。现在TT问你是否存在一个位置连续的且由26个大写字 母组成的子串，在这个子串中每个字母出现且仅出现一次，如果存在，请输出从左侧算起的第一个出现 的符合要求的子串，并且要求，如果有多组解同时符合位置最靠左，则输出字典序最小的那个解！如果 不存在，输出-1！ 这下HRZ蒙圈了，他刚学会26个字母，这对他来说太难了，所以他来求助你，请你帮 他解决这个问题，报酬是可以帮你打守望先锋。 说明：字典序 先按照第一个字母，以 A、B、C……Z 的顺序排列；如果第一个字母一样，那么比较第二 个、第三个乃至后面的字母。如果比到最后两个单词不一样长（比如，SIGH 和 SIGHT），那么把短者排 在前。例如 </p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>AB??EFGHIJKLMNOPQRSTUVWXYZ
ABCDEFGHIJKLMNOPQRSTUVWXYZ
ABDCEFGHIJKLMNOPQRSTUVWXYZ</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>上面两种填法，都可以构成26个字母，但是我们要求字典序最小，只能取前者。 注意，题目要求的是 第一个出现的，字典序最小的！ </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输入只有一行，一个符合题目描述的字符串。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出只有一行，如果存在这样的子串，请输出，否则输出-1

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Samples 
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
####  Input 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>ABC??FGHIJK???OPQR?TUVWXY?</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
#### Onput 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>ABCDEFGHIJKLMNOPQRSTUVWXYZ</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
#### Input  
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>AABCDEFGHIJKLMNOPQRSTUVW??M</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
#### Output 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>-1</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Note 
<!-- /wp:heading -->

<!-- wp:image {"id":193} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/04/捕获-3.png" alt="" class="wp-image-193"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
### Idea 
<!-- /wp:heading -->
 
分析需要找到第一个满足要求的字符串。那就让区间[i,i+25]从最左端移动，存在某个区块满足条件，才计算该区间的最小字典序值的字符串。
 判断函数只需要判断该区间存在某个字母数量多于1时就返回false,反之true，并保存字母存在的数量情况。
 计算函数需要从区间头开始遍历，发现?就用数量=0的首个字母代替，最后得到答案。  

<!-- wp:heading {"level":3} -->
### Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio> 
#include&lt;cstring>
using namespace std;
string str;
int num[26]; int p,q;
bool check(int i){
	memset(num,0,sizeof(num)); 
	p=0;q=0; 
	for(int j=i;j&lt;i+26;++j){
	  if(str[j]!='?'){
  	  p=str[j]-'A';
	  ++num[p];
	  if(num[p]>1){
	  	 return false;
	  }
	 }
	 else ++q;	
	}
	return true;
}
void getRes(int i){
	string res(26,'A');
  	p=0;
  	for(int j=i;j&lt;i+26;++j){
  	   if(str[j]=='?'){
  	   	   while(num[p]){
  	   	  	   ++p;
			}
		   res[j-i]='A'+p;
		   ++num[p];	
		}
		else res[j-i]=str[j];
	}
  cout&lt;&lt;res;
}
void getstr(){
	int len=str.size();
	for(int i=0;i&lt;len-25;++i){ 
		if(check(i)){
		 getRes(i);return;	
		} 
	}
	cout&lt;&lt;"-1";return;
}
int main(){
    cin>>str;
    if(str.size()&lt;26)cout&lt;&lt;"-1";
    else getstr();
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
## Problem  C-咕咕东的奇妙序列  
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
### Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 咕咕东 正在上可怕的复变函数，但对于稳拿A Plus的 咕咕东 来说，她早已不再听课，此时她在睡梦中 突然想到了一个奇怪的无限序列：<code style="user-select: auto;"><code style="user-select: auto;">112123123412345 ......</code></code>这个序列由连续正整数组成的若干部分构成，其 中第一部分包含1至1之间的所有数字，第二部分包含1至2之间的所有数字，第三部分包含1至3之间的所 有数字，第i部分总是包含1至i之间的所有数字。所以，这个序列的前56项会是 <code><code>11212312341234512345612345671234567812345678912345678910</code></code>，其中第1项是1，第3项是2，第20项是 5，第38项是2，第56项是0。咕咕东 现在想知道第 k 项数字是多少！但是她睡醒之后发现老师讲的东西 已经听不懂了，因此她把这个任务交给了你。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 输入由多行组成。 第一行一个整数q表示有q组询问(1&lt;=q&lt;=500)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 接下来第i+1行表示第i个输入ki,表示询问第ki项数字。 1&lt;=ki&lt;=10^18</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 输出包含q行 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>第i行输出对询问ki的输出结果。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Sample Input 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>5
1
3
20
38
56</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Sample Onput 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1
2
5
2
0</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Note 
<!-- /wp:heading -->

<!-- wp:image {"id":197} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/04/捕获-4.png" alt="" class="wp-image-197"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
### Idea 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>找规律:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1                                   ①
12
123
···
123456789
————————————————————————————————
12345678910                         ②
1234567891011
···
123456···1011···9899
————————————————————————————————
123456···1011···9899100             ③
123456··············100101</code></pre>
<!-- /wp:code -->

<!-- wp:preformatted --> 
发现从横线划开的区域各自成递增序列，第i区域每行比上一行多i个字符。那是不是可以先找到某个数n位于第i块，然后再进行更近一步的操作呢？观察发现每一区域都可以由两部分组成[矩形]+[三角形] (i=1时矩形宽度=0)。
  
虽然k的值可能非常大，但直接循环来确定区域i也可,10^18所在区域也就是十几。
   之后去解决字符在第p排的问题。由于字符所在的区域自身成等差数列,可以用二分法来找到它在第p排.这样就可以用k减去前面所有字符和，得到字符位于第q列。
   
继续想，如果知道它所在行的前面有多少个完整的段 [1-9][10-99][100-999][···(p,q)]
-->就是确定它是在几位数的段中
-->用一个循环计算出前面总共有c个数字,m个整数,该字符所在的整数是z位数
-->那就把问题简化为已知全部由z位整数组成的递增序列(从最小z位整数开始),k在第j列,求k的对应字符。

解决这个问题，我发现可以利用stringstream(设stringstream ss;)这个东东可以把数字直接转化成字符序列。
那只需要计算出k对应的数,然后把数给ss，只需要知道对应的在ss的序号即可。

这个可以先计算出k前面有p个z位整数,然后计算k对应的数是n=10^(i-1)+p,算出k的对应数位len。
把数传给ss,再把ss传给str，str[len-1]就是答案。  

<!-- wp:image {"id":216} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/04/image-5-1024x568.png" alt="" class="wp-image-216"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
### Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio> 
#include&lt;cmath>
#include&lt;sstream>
using namespace std;
typedef unsigned long long ULL; 
ULL getP(ULL n,ULL i,ULL cnts){//得到n在第i区的第p排
  ULL l=1, t, r=9*pow(10,i-1),p=-1;
   while(l&lt;=r){
   	  ULL mid=(l+r)>>1;
   	  t= (cnts+i+ cnts+i*mid)*mid/2;
   	  if(t>=n){
   	  	 p=mid;  r=mid-1;
		}
	  else l=mid+1;
   }
   return p;
} 
char getANS(const ULL j,const int i) {//i位数 ,第j列 
	stringstream ss;string str;
	ULL p= (j-1)/i;//j列所在的数的前面有p个i位数
	ULL n= pow(10,i-1)+p; 
	ss&lt;&lt;n; str=ss.str();
	ULL len=j-p*i;
	char ans=str[len-1];
	return ans;
}
void getRes(const ULL n){ 
	ULL len,lastlen,cnt,cnts,cntS,i;
	len=lastlen=cnt=cnts=cntS=i=0;
	while(++i) { 
	    cnt=9*pow(10,i-1); 
	    cnts+=(i-1)*cnt/10;
	    cntS=cnts*cnt+(i+i*cnt)*cnt/2;
	    lastlen=len;
		len+=cntS; 
		if(len>=n) break;
	}  
	ULL p=getP(n-lastlen,i,cnts); 
	ULL q= n-lastlen-cnts*(p-1) - i*p*(p-1)/2;  //在第i区的第p排的第q列  
	ULL z=0,c=0,m=0,j=1;
	while(++z){    //q在z位数的区域,该行前面共有c个数字,m个数 
		c+=9*j*z;
		m+=9*j;
		if(c>=q) break;
		j*=10;
	};
	c-=9*j*z;
	m-=9*j;  
	char ans=getANS(q-c,z);
	cout&lt;&lt;ans&lt;&lt;endl; 
}
int main(){
	int q=0; ULL k=0;
	scanf("%d",&amp;q);
	for(int i=0;i&lt;q;++i){
		scanf("%llu",&amp;k);
		getRes(k);
	}
	return 0;
}</code></pre>
<!-- /wp:code -->
