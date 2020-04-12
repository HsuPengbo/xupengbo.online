# 程序设计思维与实践 第八周      &nbsp;    [返回首页](./index.md)&nbsp;  [上篇CSP-M2](./CSP-M2.md)
##   Problem A - 区间选点 II  
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
###  Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>给定一个数轴上的 n 个区间，要求在数轴上选取最少的点使得第 i 个区间 [ai, bi] 里至少有 ci 个点 使用差分约束系统的解法解决这道题 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>多组数据。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>输入第一行一个整数 n 表示区间的个数，接下来的 n 行，每一行两个用空格隔开的整数 a，b 表示区间的左右端点。1 &lt;= n &lt;= 50000， 0 &lt;= ai &lt;= bi &lt;= 50000 并且 1 &lt;= ci &lt;= bi - ai+1。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输出一个整数表示最少选取的点的个数

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Sample Input 
<!-- /wp:heading -->

<!-- wp:code --> 
```cpp
5
3 7 3
8 10 3
6 8 1
1 3 1
10 11 1
```

<!-- wp:heading {"level":3} -->
### Sample Onput 
<!-- /wp:heading -->

<!-- wp:code -->
```cpp
6
```
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
###  Note 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Idea 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>如果用差分约束系统来解决题目，那就需要先找到所有的约束。 第 i 个区间 [ai, bi] 里至少有 ci 个点 那也就是说，如果设点i到1需要放的点数为Sum[i],就有Sum[bi]-Sum[ai-1]&gt;=ci.但是也要注意到 Sum[x]&lt;=Sum[x+1]但是Sum[x]-Sum[x-1]&lt;=1。就是说后面的点的S值肯定&gt;=前一顶点，但最多也就多1。所以整理所有约束条件：</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
```
Sum[bi]   = Sum[ai-1]+ci
Sum[i]    = Sum[i-1]+0
Sum[i-1]  = Sum[i]-1 
```
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>把从0---MAX(bi)视为图中的各个顶点，边界0视为源点，那么每个点到前一顶点的有向边距离认为必须&gt;=0,每个点到后一顶点的有向边距离必须&gt;=-1.某个点bi到点ai-1之间的距离必须&gt;=ci，可以先认为他们最开始的权就是这些限制。然后需要求在已知限制的情况下取得图中MAX(bi)点到源点的最长路径的权值和的最小解。===&gt;可以使用SPFA求最长路、判断条件设置&gt;=来处理。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>
#include&lt;iostream>
#include&lt;queue>
#include&lt;cstring>
using namespace std;
const int MAXN=200005;
const int maxn=50005;
const int inf=1e8;
int n, MAX;
struct Edge{
	int to,w,next;
}e[MAXN];
int head[maxn],sum[maxn],tot;
bool vis[maxn];
queue&lt;int> q;
void init(){
	tot=0;MAX=-1;
	memset(head,-1,sizeof(head));
}

void addEdge(int u,int v,int w){ 
	e[tot].to=v;
	e[tot].w=w;
	e[tot].next=head[u];
	head[u]=tot;
	tot++;
}
void spfa(int s) {
	for(int i = 0; i &lt;= MAX; ++i) 
		sum[i] = -inf;
	memset(vis,false,sizeof(vis));
	q.push(s); sum[s] = 0; vis[s] = true;  
	while(!q.empty()) {
		int u = q.front(); q.pop(); 
		vis[u] = false; 
		 for(int i = head[u]; i!=-1; i = e[i].next) {
			int v = e[i].to;  
			if(sum[v] &lt; sum[u] + e[i].w) {
				sum[v] = sum[u] + e[i].w; 
				if(!vis[v]) {
					q.push(v);
					vis[v] = true;
				}
			}
		 } 
	}
	cout&lt;&lt;sum[MAX]; 
}
int main(){
    scanf("%d",&amp;n);
    int u,v,w;
    init();
    for(int i=0;i&lt;n;++i){
    	scanf("%d%d%d",&amp;u,&amp;v,&amp;w); 
		MAX=v>MAX?v:MAX;
    	addEdge(u-1,v,w); 
    }   
    for(int i=1;i&lt;=MAX;++i) {
    	addEdge(i-1,i,0);
    	addEdge(i,i-1,-1);
	}
    spfa(0);
	return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
##   Problem B - 猫猫向前冲 
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
###  Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>  众所周知， TT 是一位重度爱猫人士，他有一只神奇的魔法猫。<br>有一天，TT 在 B 站上观看猫猫的比赛。一共有 N 只猫猫，编号依次为1，2，3，…，N进行比赛。比赛结束后，Up 主会为所有的猫猫从前到后依次排名并发放爱吃的小鱼干。不幸的是，此时 TT 的电子设备遭到了宇宙射线的降智打击，一下子都连不上网了，自然也看不到最后的颁奖典礼。<br>不幸中的万幸，TT 的魔法猫将每场比赛的结果都记录了下来，现在他想编程序确定字典序最小的名次序列，请你帮帮他。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

输入有若干组，每组中的第一行为二个数N（1&lt;=N&lt;=500），M；其中N表示猫猫的个数，M表示接着有M行的输入数据。接下来的M行数据中，每行也有两个整数P1，P2表示即编号为 P1 的猫猫赢了编号为 P2 的猫猫。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

给出一个符合要求的排名。输出时猫猫的编号之间有空格，最后一名后面没有空格!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>其他说明：符合条件的排名可能不是唯一的，此时要求输出时编号小的队伍在前；输入数据保证是正确的，即输入数据确保一定能有一个符合要求的排名。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Sample Input 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4 3
1 2
2 3
4 3</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
###  Sample Onput 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1 2 4 3</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Idea 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>拓扑排序问题，另外需要注意要求最小字典序。拓扑排序可以用Kahn算法。</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->

将所有入度=0的点组成集合。
• 每次从 S 里面取出一个顶点 u （可以随便取）放入 L , 然后遍历顶点 u 的 所有边 (u, v) , 并删除之，并判断如果该边的
另一个顶点 v，如果在移除 这一条边后入度为 0 , 那么就将这个顶点放入集合 S 中。不断地重复取 出顶点然后重复这个过程
• 最后当集合为空后，就检查图中是否存在任何边。如果有，那么这个图 一定有环路，否者返回 L , L 中顺序就是拓扑排序的结果
<p>由于要确保最小字典序，这里我选择了优先级队列(升序)。每次把最小的入度=0的顶点从队列取出，保证了在排序合理的情况下能够让编号偏小的队伍在前。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;queue>
#include&lt;vector>
#include&lt;cstring>
using namespace std;
const int MAXN=505;
const int MAXM=5000;
int N,M;
struct Edge{
	int to,next;
}e[MAXM];
int head[MAXN],InDeg[MAXN],tot;
bool vis[MAXM];
struct cmp{
   bool operator()(int r, int l){ return r>l; } 
};
priority_queue&lt;int,vector&lt;int>,cmp > q;
vector&lt;int> ans;
void init(){
	tot=0;
	memset(head,-1,sizeof(head));
	memset(InDeg,0,sizeof(InDeg));
	ans.clear();
}
void addEdge(int p1,int p2){ 
	e[tot].to=p2; 
	e[tot].next=head[p1];
	head[p1]=tot;
	++InDeg[p2];
	tot++;
} 
void Kahn(){
	for(int i=1;i&lt;=N;++i){
		if(!InDeg[i]) q.push(i);
	}
	memset(vis,true,sizeof(vis));
	while(q.size()){
		int p1=q.top(); q.pop();
		ans.push_back(p1);
		for(int i = head[p1]; i!=-1; i = e[i].next){
		  int p2 = e[i].to;
		  if(vis[i]){
		  	 if(--InDeg[p2]==0) q.push(p2);
		  	 vis[i]=false;//边被删除 
		  }	
		}
	}
	cout&lt;&lt;ans[0]; 
	for(int i=1;i&lt;N;++i) cout&lt;&lt;" "&lt;&lt;ans[i];
	cout&lt;&lt;endl; 
}
int main(){ 
    int p1,p2;
	while(~scanf("%d%d",&amp;N,&amp;M)) {
      init();
	  for(int i=0;i&lt;M;++i){
		scanf("%d%d",&amp;p1,&amp;p2);
		addEdge(p1,p2);
	  }
	  Kahn();
	} 
    return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
##  Problem C -  班长竞选  
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
### Description 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

大学班级选班长，N 个同学均可以发表意见 若意见为 A B 则表示 A 认为 B 合适，意见具有传递性，即 A 认为 B 合适，B 认为 C 合适，则 A 也认为 C 合适 勤劳的 TT 收集了M条意见，想要知道最高票数，并给出一份候选人名单，即所有得票最多的同学，你能帮帮他吗？

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
### Input 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

本题有多组数据。第一行 T 表示数据组数。每组数据开始有两个整数 N 和 M (2 &lt;= n &lt;= 5000, 0 &lt;m &lt;= 30000)，接下来有 M 行包含两个整数 A 和 B(A != B) 表示 A 认为 B 合适。

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Output 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>

对于每组数据，第一行输出 “Case x: ”，x 表示数据的编号，从1开始，紧跟着是最高的票数。 接下来一行输出得票最多的同学的编号，用空格隔开，不忽略行末空格！

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Sample Input 
<!-- /wp:heading -->

<!-- wp:code -->
```cpp
2
4 3
3 2
2 0
2 1

3 3
1 0
2 1
0 2
```
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
###  Sample Onput 
<!-- /wp:heading -->

<!-- wp:code -->
```cpp
Case 1: 2
0 1
Case 2: 2
0 1 2
```
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
### Note 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>PE多次，这次题目说的不要忽略行末空格我以为是行末空格也要带上，然而并不是。另外刚开始写了一遍然后运行发现一个样例都没有得到正确结果，之后分析是把后序，逆后序，生成的SCC编号之间的对应关系搞错了。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
###  Idea 
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>整体思路:如果把每个人看作一个点，那么那些互相可以通过意见传递发现两个人意见相互连通，那他们受到的支持票数是一样的。这些点就相当于一个有向图中的强连通分量。我们就可以先把点缩小至对应的强连通分量，因为一个分量中的点的票数都是一样的。找到强连通分量后，在原图遍历所有出度=0的强连通分量SCC(也就是反图的入度=0的SCC)。答案必然在这样的SCC中，所以只需要遍历每个入度=0的SCC，然后DFS计算能够到达的所有SCC，然后记得初始-1，因为本人不能给自己投票。</p>
<!-- /wp:paragraph -->
具体：

<!-- wp:preformatted -->
1.求SCC需要DFS得到后序序列，然后从后序序列的最后一个点往前DFS，如过遍历点时没有标记就说明是新的SCC，那些在逆后序序列中可以
从一个点访问到的都是同一个SCC。
2.遍历图中所有边，当边的两个顶点不属于同一SCC，from点[反图就是to点]所属的SCC出度[反图的入度]+1。  
3.遍历所有点i，当 c[i] (所属的SCC)的入度InDeg[c[i]]=0，开始遍历寻找能够到达的所有SCC j，然后把他们的点数scc[j]都加到ANS[c[i]]
中，每次遍历完成后更新最大值。  
4.遍历所有点，当对应的SCC的ANS值等于最大值时，打印
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
### Codes 
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
#include&lt;vector>
#include&lt;cstring>
using namespace std;
const int MAXN=5005;
const int MAXM=30005;
int N,M;
struct Edge{
	int from,to,next;
}e1[MAXM],e2[MAXM];
int head1[MAXN],head2[MAXN],dfn[MAXN];
int scnt,c[MAXN],scc[MAXN],Out[MAXN],InDeg[MAXN];//scnt=scc数量,c[i]表示第i号同学处于c[i]号SCC中 InDeg是SCC入
int dcnt,tot; bool vis[MAXN],vic[MAXN];
int ans[MAXN];
void init(){
	tot=0;
	memset(head1,-1,sizeof(head1));
	memset(head2,-1,sizeof(head2));
    memset(Out,0,sizeof(Out));
}
void addEdge(int u,int v){ 
	e1[tot].from=u;e1[tot].to=v;   e1[tot].next=head1[u];  //正图 
	head1[u]=tot; 
	e2[tot].from=v; e2[tot].to=u;   e2[tot].next=head2[v];  //反图 
	head2[v]=tot; ++Out[u];  tot++;
}
void dfs1(int x){
	vis[x]=true;
	for(int i=head1[x];i!=-1;i=e1[i].next){
		if(!vis[e1[i].to]) dfs1(e1[i].to); 
    }
	dfn[dcnt++]=x;
}
void dfs2(int x){
	c[x]=scnt; ++scc[scnt];//第scnt号scc加一 
	for(int i=head2[x];i!=-1;i=e2[i].next){
	 if(!c[e2[i].to]) dfs2(e2[i].to);	
	}
}
void dfs(int x,int j){//j表示 源 强连通分量 
   vis[x]=true; 
   if(!vic[c[x]]) ans[j]+= scc[c[x]]; vic[c[x]]=true;
   for(int i=head2[x];i!=-1;i=e2[i].next){
   	 if(!vis[e2[i].to]) dfs(e2[i].to,j);
   }
}
void getCase(){
	dcnt=scnt=0;
	memset(scc,0,sizeof(scc));
	memset(vis,false,sizeof(vis));
	memset(c,0,sizeof(c)); 
	memset(InDeg,0,sizeof(InDeg)); 
	memset(ans,-1,sizeof(ans));
	for(int i=0;i&lt;N;++i){
		if(!vis[i]) dfs1(i);
	} 
	for(int i=N-1;i>=0;--i){ //逆后序 
	   if(!c[dfn[i]]){
	   	++scnt; dfs2(dfn[i]);  //得到scnt个scc,i点的scc编号是c[i] 
	   }
	} 
	for(int i=0;i&lt;M;++i){
	  int fr=e1[i].from,to=e1[i].to;
	  if(c[fr]!=c[to])  ++InDeg[c[fr]];
	} 
    int j=0,maxm=-1;
	for(int i=0;i&lt;N;++i){
    	j=c[i];
		if(!InDeg[j]){
		memset(vis,false,sizeof(vis));
		memset(vic,false,sizeof(vic));	
		  dfs(i,j); InDeg[j]=1;
		  if(maxm&lt;ans[j]) {  maxm=ans[j]; }
		}
	}
	cout&lt;&lt;maxm&lt;&lt;endl;bool tag=false;
	for(int i=0;i&lt;N;++i){
		if(ans[c[i]]==maxm){
		 if(tag) cout&lt;&lt;" "; tag=true;
		 cout&lt;&lt;i;	
		} 
	} cout&lt;&lt;endl;
}
int main(){
	int T,A,B; scanf("%d",&amp;T); 
	for(int i=1;i&lt;T+1;++i){
	    init();
		scanf("%d%d",&amp;N,&amp;M);
		for(int j=0;j&lt;M;++j){
			scanf("%d%d",&amp;A,&amp;B);
			addEdge(A,B);
		}
		cout&lt;&lt;"Case "&lt;&lt;i&lt;&lt;": ";
		getCase();
	}
	return 0;
}</code></pre>
<!-- /wp:code -->
# 结束      &nbsp;    [返回首页](./index.md)&nbsp;  [下篇待定]
