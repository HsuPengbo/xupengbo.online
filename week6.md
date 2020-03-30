# 程序设计思维与实践 第6周
<!-- wp:heading -->
<h2>Problem A- - 氪金带东 </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3> Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>实验室里原先有一台电脑(编号为1)，最近氪金带师咕咕东又为实验室购置了N-1台电脑，编号为2到N。每台电脑都用网线连接到一台先前安装的电脑上。但是咕咕东担心网速太慢，他希望知道第i台电脑到其他电脑的最大网线长度，但是可怜的咕咕东在不久前刚刚遭受了宇宙射线的降智打击，请你帮帮他。<br></p>
<!-- /wp:paragraph -->

<!-- wp:image {"width":297,"height":243} -->
<figure class="wp-block-image is-resized"><img src="https://s1.ax1x.com/2020/03/25/8XylFS.png" alt="" width="297" height="243"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>提示: 样例输入对应这个图，从这个图中你可以看出，距离1号电脑最远的电脑是4号电脑，他们之间的距离是3。 4号电脑与5号电脑都是距离2号电脑最远的点，故其答案是2。5号电脑距离3号电脑最远，故对于3号电脑来说它的答案是3。同样的我们可以计算出4号电脑和5号电脑的答案是4.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Input </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>输入文件包含多组测试数据。对于每组测试数据，第一行一个整数N (N&lt;=10000)，接下来有N-1行，每一行两个数，对于第i行的两个数，它们表示与i号电脑连接的电脑编号以及它们之间网线的长度。网线的总长度不会超过10^9，每个数之间用一个空格隔开。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph {"align":"left"} -->
<p style="text-align:left">对于每组测试数据输出N行，第i行表示i号电脑的答案 (1&lt;=i&lt;=N).</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>5
1 1
2 1
3 1
1 1</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>3
2
3
4
4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:image {"id":100} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/03/image-9-1024x617.png" alt="" class="wp-image-100"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio>  
#include&lt;algorithm>
#include&lt;cstring>
using namespace std;
const int MAXN=100005; 
int n,maxL,maxit,far1,far2,ans;
int Len1[MAXN],Len2[MAXN];int u,w;
struct Edge{
	int u,v,w,nxt;
}Edges[MAXN];
int head[MAXN],tot; bool vis[MAXN];
void init(){
	tot=0;
	for(int i=0;i&lt;n+2;++i) head[i]=-1;
}
void addEdge(int u,int v,int w){
	Edges[tot].u=u;
	Edges[tot].v=v;
	Edges[tot].w=w;
	Edges[tot].nxt=head[u];
	head[u]=tot;
	tot++;
}
void input(){
	init();
	for(int i=2;i&lt;=n;++i){
		scanf("%d%d",&amp;u,&amp;w);
		addEdge(i,u,w);
		addEdge(u,i,w);
	}
}
void dfsLen(int u,int *a,int L){  
   a[u]=L; 
   if(maxL&lt;L) {
  	 maxL=L;maxit=u;
   }
   for(int i=head[u];i!=-1;i=Edges[i].nxt){
  	if(!vis[Edges[i].v]){ 
  		vis[Edges[i].v]=true; 
  		dfsLen(Edges[i].v, a, L + Edges[i].w);
	  }
  } 
} 
void output(){    //输出每个点到其他点的最大距离 
	memset(vis,false,sizeof(vis)); maxL=-1;vis[1]=true;
	dfsLen(1,Len1,0);    far1=maxit;
	memset(vis,false,sizeof(vis)); maxL=-1;vis[far1]=true;
	dfsLen(far1,Len1,0); far2=maxit;
    memset(vis,false,sizeof(vis));vis[far2]=true;
    dfsLen(far2,Len2,0);
    for(int i=1;i&lt;=n;i++){
    	ans=max(Len1[i],Len2[i]);
    	printf("%d\n",ans);
	}
} 
int main(){
	while(~scanf("%d",&amp;n)){
	 input(); 
	 output();	
	}
	return 0;
} </code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem  B - 戴好口罩  </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3> Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>新型冠状病毒肺炎（Corona Virus Disease 2019，COVID-19），简称“新冠肺炎”，是指2019新型冠状病毒感染导致的肺炎。<br>如果一个感染者走入一个群体，那么这个群体需要被隔离！<br>小A同学被确诊为新冠感染，并且没有戴口罩！！！！！！<br>危！！！<br>时间紧迫！！！！<br>需要尽快找到所有和小A同学直接或者间接接触过的同学，将他们隔离，防止更大范围的扩散。<br>众所周知，学生的交际可能是分小团体的，一位学生可能同时参与多个小团体内。<br>请你编写程序解决！戴口罩！！ </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input  </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>多组数据，对于每组测试数据：<br>第一行为两个整数n和m（n = m = 0表示输入结束，不需要处理），n是学生的数量，m是学生群体的数量。0 &lt; n &lt;= 3e4 ， 0 &lt;= m &lt;= 5e2<br>学生编号为0~n-1<br>小A编号为0<br>随后，m行，每行有一个整数num即小团体人员数量。随后有num个整数代表这个小团体的学生。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>输出要隔离的人数，每组数据的答案输出占一行 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>100 4
2 1 2
5 10 13 11 12 14
2 0 1
2 99 2
200 2
1 5
5 1 2 3 4 5
1 0
0 0</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4
1
1</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>分析该题是并查集的简单应用。题目需要找到所有0点能够走到的点的数<br>目，当然可以用BFS或者DFS遍历得到，但是不快。                                                     适合用并查集，即先将各点的源点设为自身，然后在分组输入的时候，把同组其他点每组第一个点合并成一个集合，同时用另一个存放每个源点所拥有的集合元素数目。最后只需要寻找到0点的源点，输出其所在集合的元素数目即可。由于需要多次输入输出，所以一定要记得每次的初始化。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
#include&lt;cstdio>
using namespace std;
const int MAXN=30005;
int par[MAXN],rnk[MAXN], Num[600],n,m,sum;
void init(){
	for(int i=0;i&lt;n;++i){
	 par[i]=i; rnk[i]=1;
	} 
}
int find(int x){
	if(par[x]==x)
	  return x;
	return par[x]=find(par[x]);
}
void unite(int x,int y){
	x=find(x);y=find(y);
	if(x==y) return;
	if(rnk[x]>rnk[y]) swap(x,y);
	par[x]=y; rnk[y] += rnk[x]; 
}
void input(){
	init(); int u,v,num;
	for(int i=0;i&lt;m;++i){
		scanf("%d%d",&amp;num,&amp;u); 
		for(int j=1;j&lt;num;++j){
			scanf("%d",&amp;v);   unite(u,v);
		}
	}
} 
void output(){
	int p=find(0);
	sum=rnk[p];
	printf("%d\n",sum);
}
int main(){
	while(~scanf("%d%d",&amp;n,&amp;m)){
		if(n==0 &amp;&amp;m==0) break;
	  input();
	  output();	
	}
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>  Problem C - 掌握魔法的东东 I</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3> Description  </h3>
<!-- /wp:heading -->

<!-- wp:paragraph {"fontSize":"small"} -->
<p class="has-small-font-size">东东在老家农村无聊，想种田。农田有 n 块，编号从 1~n。种田要灌溉。众所周知东东是一个魔法师，他可以消耗一定的 MP 在一块田上施展魔法，使得黄河之水天上来。他也可以消耗一定的 MP 在两块田的渠上建立传送门，使得这块田引用那块有水的田的水。 (1&lt;=n&lt;=3e2)黄河之水天上来的消耗是 Wi，i 是农田编号 (1&lt;=Wi&lt;=1e5)<br>建立传送门的消耗是 Pij，i、j 是农田编号 (1&lt;= Pij &lt;=1e5, Pij = Pji, Pii =0)<br>东东为所有的田灌溉的最小消耗 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>

Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第1行：一个数n<br>第2行到第n+1行：数wi<br>第n+2行到第2n+1行：矩阵即pij矩阵</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>东东最小消耗的MP值</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Example</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4
5
4
4
3
0 2 2 2
2 0 3 3
2 3 0 4
2 3 4 0</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>9</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>如果把传送门代价视为树中两点之间的边的权值，那么问题貌似就转变为求最小生成树。但是“黄河之水天上来”怎么办？发现每个点到天上的代价也给出来，那就可以视为还存在一个点o,o点到其他点的边权值就是从天上得到黄河水的代价。即一个图有0,1,···,n共n+1个点，点和点之间的有权边也知道，MP就是代价最小的生成树。此处就可以用krusal或者priem算法求出最小生成树的代价和。这里我用krusal法，利用并查集+贪心实现该算法。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>krusal算法过程:(n+1条边,并查集)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>(1)将所有边按权值升序排序。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>(2)遍历每条边，如果取出的边不和已经保留的边形成环路(判断边的端点是否属于同一集合)，就保留该边(两点合并到一个集合里)，不然就放弃。当边的数目达到n时停止。[树的边数=点数-1]</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
#include&lt;cstdio>
using namespace std;
const int MAXN=305;
int par[MAXN], rnk[MAXN], n, Size;
struct Edge{
	int u,v,w;	
	bool operator&lt;(Edge e){
		return w&lt;e.w;
	}
}Edges[MAXN * MAXN];
void addEdge(int u,int v,int w){
	Edges[Size].u=u; Edges[Size].v=v;
	Edges[Size].w=w; ++Size;
}
void init(){
    Size=0;
	for(int i=0;i&lt;n+1;++i){
	 par[i]=i; rnk[i]=1;
	} 
}
int find(int x){
	if(par[x]==x)
	  return x;
	return par[x]=find(par[x]);
}
bool unite(int x,int y){
	x=find(x);y=find(y);
	if(x==y) return false;
	if(rnk[x]>rnk[y]) swap(x,y);
	par[x]=y; rnk[y] += rnk[x]; 
	return true;
} 
void input(){
	scanf("%d",&amp;n); init(); int wi;
	for(int i=1;i&lt;n+1;++i){
		scanf("%d",&amp;wi); addEdge(0,i,wi);
	}
	for(int i=1;i&lt;n+1;++i){
		for(int j=1;j&lt;n+1;++j){
			scanf("%d",&amp;wi);
			if(i!=j)  addEdge(i,j,wi); 
		}
	}
}
void output(){
	sort(Edges,Edges+Size);
	int sum=0,tot=0; int u,v;
	for(int i=0;i&lt;Size;++i){
	  u=Edges[i].u; v=Edges[i].v;
	  if(unite(u,v)){
	  	sum+=Edges[i].w; ++tot; //printf("(%d,%d)",u,v); 
	  }	
	  if(tot==n) break;	
	}
	printf("%d",sum);
}
int main(){
	input();
	output();
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>Problem D - 数据中心 </h2>
<!-- /wp:heading -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://s1.ax1x.com/2020/03/23/87zdlq.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Example</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4
5
1
1 2 3
1 3 4
1 4 5
2 3 8
3 4 2</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://s1.ax1x.com/2020/03/23/87zHtH.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>该题仍然可以选择用krusal来取最小生成树，如果root点同时还在最大权值的边的一端，那么最大权值就是最长时间。所以我们需要做的事情就是在得到最小生成树的过程中记录最大边。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
#include&lt;cstdio>
using namespace std;
const int MAXN=50005,MAXM=100010;
int par[MAXN], rnk[MAXN], n, m, root, Size;
struct Edge{
	int u,v,w;	
	bool operator&lt;(Edge e){
		return w&lt;e.w;
	}
}Edges[MAXM];
void addEdge(int u,int v,int w){
	Edges[Size].u=u; Edges[Size].v=v;
	Edges[Size].w=w; ++Size;
}
void init(){
    Size=0;
	for(int i=0;i&lt;n+1;++i){
	 par[i]=i; rnk[i]=1;
	} 
}
int find(int x){
	if(par[x]==x)
	  return x;
	return par[x]=find(par[x]);
}
bool unite(int x,int y){
	x=find(x);y=find(y);
	if(x==y) return false;
	if(rnk[x]>rnk[y]) swap(x,y);
	par[x]=y; rnk[y] += rnk[x]; 
	return true;
} 
void input(){
	scanf("%d%d%d",&amp;n,&amp;m,&amp;root);
	init(); int u,v,w;
	for(int i=0;i&lt;m;++i){
		scanf("%d%d%d",&amp;u,&amp;v,&amp;w); addEdge(u,v,w);
	} 
}
void output(){
	sort(Edges,Edges+m);
	int ans=0,tot=0; int u,v;
	for(int i=0;i&lt;m;++i){
	  u=Edges[i].u; v=Edges[i].v;
	  if(unite(u,v)){
	  	ans=max(ans,Edges[i].w); ++tot; //printf("(%d,%d)",u,v); 
	  }	
	  if(tot==n-1) break;	
	}
	printf("%d",ans);
}
int main(){
	input();
	output();
	return 0;
}</code></pre>
<!-- /wp:code -->
