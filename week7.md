# 程序设计思维与实践 第七周        &nbsp;    [返回首页](./index.md)&nbsp;  [上篇 Week6](./week6.md)
<!-- wp:heading -->
<h2>  Problem  A - TT 的魔法猫 </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>众所周知，TT 有一只魔法猫。
这一天，TT 正在专心致志地玩《猫和老鼠》游戏，然而比赛还没开始，聪明的魔法猫便告诉了 TT 比赛的最终结果。TT 非常诧异，不仅诧异于他的小猫咪居然会说话，更诧异于这可爱的小不点为何有如此魔力？
魔法猫告诉 TT，它其实拥有一张游戏胜负表，上面有 N 个人以及 M 个胜负关系，每个胜负关系为 A B，表示 A 能胜过 B，且胜负关系具有传递性。即 A 胜过 B，B 胜过 C，则 A 也能胜过 C。
TT 不相信他的小猫咪什么比赛都能预测，因此他想知道有多少对选手的胜负无法预先得知，你能帮帮他吗？</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行给出数据组数。
每组数据第一行给出 N 和 M（N , M &lt;= 500）。
接下来 M 行，每行给出 A B，表示 A 可以胜过 B。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对于每一组数据，判断有多少场比赛的胜负不能预先得知。注意 (a, b) 与 (b, a) 等价，即每一个二元组只被计算一次。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>3
3 3
1 2
1 3
2 3
3 2
1 2
2 3
4 2
1 2
3 4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>0
0
4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">这道题是求取任意两点之间的胜负关系，属于传递闭包问题。
如果两点之间没法判断胜负关系说明不在一个闭包关系里，可以使用Floyd算法实现。
当dis[a][b]=1、0分别说明强关系、关系未知。
最后遍历所有的点，dis[a][b]、dis[b][a]都为0时说明没法判断，++ans。</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio>
#define _for(i,a,b) for(int i=(a);i&lt;(b);++i)
using namespace std;
int P,N,M;
int dis[505][505];
void init(int n){
	_for(i,1,n)
	  _for(j,1,n)
	   dis[i][j]=0; 
}
void Floyd(int n){
   _for(k,1,n){
       _for(i,1,n){
          if(dis[i][k])
	     _for(j,1,n)
  	     dis[i][j]=(dis[i][j])||( dis[i][k] &amp;&amp; dis[k][j] );
       }
   }
}
void out(int n){
   int ans=0;
     _for(i,1,n)
	_for(j,i+1,n){
	  if(dis[i][j]==0 &amp;&amp; dis[j][i]==0) ++ans;
        } 
   cout&lt;&lt;ans&lt;&lt;endl;
}
int main(){
   cin>>P; int A,B;
   while(P--){
	cin>>N>>M;
	init(N+1); 
	_for(i,0,M){
	  cin>>A>>B;
	  dis[A][B]=1;	
	}
	Floyd(N+1);
	out(N+1); 
   }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2>  Problem  B - TT 的旅行日记</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>众所周知，TT 有一只魔法猫。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>今天他在 B 站上开启了一次旅行直播，记录他与魔法猫在喵星旅游时的奇遇。 TT 从家里出发，准备乘坐猫猫快线前往喵星机场。猫猫快线分为经济线和商业线两种，它们的速度与价钱都不同。当然啦，商业线要比经济线贵，TT 平常只能坐经济线，但是今天 TT 的魔法猫变出了一张商业线车票，可以坐一站商业线。假设 TT 换乘的时间忽略不计，请你帮 TT 找到一条去喵星机场最快的线路，不然就要误机了！</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 输入包含多组数据。每组数据第一行为 3 个整数 N, S 和 E (2 ≤ N ≤ 500, 1 ≤ S, E ≤ 100)，即猫猫快线中的车站总数，起点和终点（即喵星机场所在站）编号。  </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>下一行包含一个整数 M (1 ≤ M ≤ 1000)，即经济线的路段条数。 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 接下来有 M 行，每行 3 个整数 X, Y, Z (1 ≤ X, Y ≤ N, 1 ≤ Z ≤ 100)，表示 TT 可以乘坐经济线在车站 X 和车站 Y 之间往返，其中单程需要 Z 分钟。 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 下一行为商业线的路段条数 K (1 ≤ K ≤ 1000)。 </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 接下来 K 行是商业线路段的描述，格式同经济线。  </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>所有路段都是双向的，但有可能必须使用商业车票才能到达机场。保证最优解唯一。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对于每组数据，输出3行。第一行按访问顺序给出 TT 经过的各个车站（包括起点和终点），第二行是 TT 换乘商业线的车站编号（如果没有使用商业线车票，输出"Ticket Not Used"，不含引号），第三行是 TT 前往喵星机场花费的总时间。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>本题不忽略多余的空格和制表符，且每一组答案间要输出一个换行</strong></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>4 1 4
4
1 2 2
1 3 3
2 4 4
3 4 5
1
2 4 3</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1 2 4
2
5</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">该题属于没有负边的单源最短路径问题。车站就是顶点，路线就是有权边，可以选择 Dijkstra 算法。
设置源点s,初始化各点到远点的距离数组dis[]为无限大,然后将dis[s]置为0。
将源点加入最小堆。
取出堆中点x,遍历x的邻接边。比较dis[y]>dis[x]+w,如果满足条件就松弛操作。
堆空时得到最短距离数组dis[]</pre>
<!-- /wp:preformatted -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">由于我们还需要保存路径,所以需要建立数组path,每次在更新dis[y]时,也加上path[y]=x;保存y的上一个点x。
（但是递归输出的顺序刚好相反。）
将S作为源点求出各点到其最短路径,得到dis1[]、path1[]。
将E作为源点求出各点到其最短路径,得到dis2[]、path2[]。
遍历所有商业线，设定u=0,v=0;
每次将走商业线(X,Y,Z)的dis1[X]+dis2[Y]+W、dis1[Y]+dis2[X]+Z和不走的dis2[S](S到E的路径)三者进行比较，
    如果走了商业线的话记得更新u,v然后分情况输出。
    如果u=0说明没有走商业线，输出时使用path2[S]，将从起点S到终点E的路径顺序输出。
反之走了商业线，用path1[]输出从起点S到点u,用path2[]输出点v到终点E。
(path1[]如果先打印后递归时顺序是倒着的，所以递归函数中需要先递归后打印。path2[]先打印后递归。)
另外需要记得空格、空行问题，这道题我PE了很多次，最后发现每组数据之间需要另外空一行。</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream> 
#include&lt;cstring>
#include&lt;queue> 
#define _for(i,a,b) for(int i=(a);i&lt;(b);++i)
using namespace std;
const int MAXM=2010;
const int MAXN=505;
const int inf=1000000;
int N,S,E,M,K;
struct Edge{  //普通有向边 
	int to,next,w;
}e[MAXM];
struct CEdge{ //商业线 
 int a,b,w;	
}ce[1010];
int head[MAXN],tot1,tot2,dis1[MAXN],dis2[MAXN]; 
bool vis[MAXN]; int path1[MAXN],path2[MAXN]; int cnt[MAXN];
priority_queue&lt;pair&lt;int,int> > q; 
void adde(int x,int y,int w){
    e[++tot1].to=y; e[tot1].next=head[x];
    e[tot1].w=w; head[x]=tot1;
}
void addce(int x,int y,int w){
    ce[++tot2].a=x;
    ce[tot2].b=y;
    ce[tot2].w=w;
}
void init(){
    memset(head,0,sizeof(head)); 
    memset(path1,0,sizeof(path1));
    memset(path2,0,sizeof(path2));
} 
void dijkstra(int s,int *dis,int *path){
    _for(i,1,N+1) dis[i]=inf;  dis[s]=0;  
    memset(vis,false,sizeof(vis));
    while(q.size()) q.pop();
	q.push(make_pair(0,s));
	while(q.size()){
    	int x=q.top().second;
    	q.pop();
    	if(vis[x])continue;
    	vis[x]=true;
    	for(int i=head[x];i;i=e[i].next){
    	    int y=e[i].to,w=e[i].w; 
    	    if(dis[y]>dis[x]+w){
    	    	dis[y]=dis[x]+w;
    	    	q.push(make_pair(-dis[y],y));
    	    	path[y]=x;
    	    }
    	}
    }
}
void dfs1(int k,int s){
    if(k==0) return;	 
    dfs1(path1[k],s);
    if(s==k) printf("%d",k);
    else printf("%d ",k);
}
void dfs2(int k,int s){
    if(k==0) {
      return;	
    }
    if(k==s) printf("%d",k); 	
    else printf(" %d",k);
    dfs2(path2[k],s);
}
int main(){
    int X,Y,Z,T=0;
    while(~scanf("%d%d%d",&amp;N,&amp;S,&amp;E)){
    	if(T!=0 )printf("\n"); T++;
    init();
    	tot1=tot2=0; 
    	scanf("%d",&amp;M);
    	while(M--){
        	scanf("%d%d%d",&amp;X,&amp;Y,&amp;Z);
    		adde(X,Y,Z); adde(Y,X,Z);
    	}
    	scanf("%d",&amp;K);
    	while(K--){
    		scanf("%d%d%d",&amp;X,&amp;Y,&amp;Z);
    		addce(X,Y,Z);
    	}
    	dijkstra(S,dis1,path1);//S点到所有点的最短距离  
    	dijkstra(E,dis2,path2);
    	int ans= dis1[E],tmp=0; 
    	int u=0,v=0;
    	for(int i=1;i&lt;=tot2;++i){
    	    X=ce[i].a;Y=ce[i].b;Z=ce[i].w;
    	    tmp=dis1[X]+dis2[Y]+Z;
    	    if(tmp&lt;ans){
    	     ans=tmp; u=X;v=Y;
    	    }
    	    tmp=dis1[Y]+dis2[X]+Z;
    	    if(tmp&lt;ans) {
    	      ans=tmp; u=Y;v=X;
    	    }
    	} 
    	if(u==0){
        dfs2(S,S);printf("\n");
         printf("Ticket Not Used\n%d\n",ans);
    	}
    	else{
    	 dfs1(u,u);printf(" ");dfs2(v,v);printf("\n");
    	 printf("%d\n%d\n",u,ans);
    	}  
    }
    return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p> </p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>  Problem C - TT 的美梦 </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>这一晚，TT 做了个美梦！   

在梦中，TT 的愿望成真了，他成为了喵星的统领！喵星上有 N 个商业城市，编号 1 ～ N，其中 1 号城市是 TT 所在的城市，即首都。

喵星上共有 M 条有向道路供商业城市相互往来。但是随着喵星商业的日渐繁荣，有些道路变得非常拥挤。正在 TT 为之苦恼之时，他的魔法小猫咪提出了一个解决方案！TT 欣然接受并针对该方案颁布了一项新的政策。

具体政策如下：对每一个商业城市标记一个正整数，表示其繁荣程度，当每一只喵沿道路从一个商业城市走到另一个商业城市时，TT 都会收取它们（目的地繁荣程度 - 出发地繁荣程度）^ 3 的税。

TT 打算测试一下这项政策是否合理，因此他想知道从首都出发，走到其他城市至少要交多少的税，如果总金额小于 3 或者无法到达请悄咪咪地打出 '?'。 </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行输入 T，表明共有 T 组数据。（1 &lt;= T &lt;= 50） </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>对于每一组数据，第一行输入 N，表示点的个数。（1 &lt;= N &lt;= 200）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 第二行输入 N 个整数，表示 1 ～ N 点的权值 a[i]。（0 &lt;= a[i] &lt;= 20） </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>第三行输入 M，表示有向道路的条数。（0 &lt;= M &lt;= 100000）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 接下来 M 行，每行有两个整数 A B，表示存在一条 A 到 B 的有向道路。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 接下来给出一个整数 Q，表示询问个数。（0 &lt;= Q &lt;= 100000）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 每一次询问给出一个 P，表示求 1 号点到 P 号点的最少税费。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>每个询问输出一行，如果不可达或税费小于 3 则输出 '?'。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Sample Input</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>2
5
6 7 8 9 10
6
1 2
2 3
3 4
1 5
5 4
4 5
2
4
5
10
1 2 4 4 5 6 7 8 9 10
10
1 2
2 3
3 1
1 4
4 5
5 6
6 7
7 8
8 9
9 10
2
3 10</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Sample Output</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>Case 1:
3
4
Case 2:
?
?</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">可以将商业城市看作顶点,收取的费用视为边权,给定的单向路线视为有向边。则题目属于单源最短路径问题。
由于税收值可能为负值,即图中可能出现负权边,可以采用SPFA方法来解决带负权边的单源最短路径问题。
1.将起点作为源点,加入队列中。
2.每次从队列中取出队首u,遍历邻接边的点v。
    如果dis[v]>dis[u]+w,就更新dis[v]=dis[u]+w，另外保存前置点pre[v]=u。
    由于可能出现负权边,所以为了防止出现负环,需要设置cnt[]数组保存从源点到达点v时经过的点数cnt[v]。
    如果cnt[v]>=n说明出现负环，要另外数组noPath[]，将noPath[v]判为true，即不能到达。
3.最后查询时如果noPath[v]=true或者dis[v]&lt;3或者dis[v]=INF都输出"?",反之输出对应dis[v]。</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;cstdio>
#include&lt;cstring>
#include&lt;queue> 
#include&lt;cmath>
#define _for(i,a,b) for(int i=(a);i&lt;(b);++i)
using namespace std;
const int maxn=210;
const int maxm=200010;
const int INF=1000000;
int W[maxn];
int T,N,M,Q,P,tot;
struct Edge{  
	int to,next,w;
}e[maxm]; 
int head[maxn],pre[maxn],inq[maxn],cnt[maxn],dis[maxn];
bool noPath[maxn];
queue&lt;int> q; 
void addedge(int A,int B,int w){
    e[++tot].to=B; e[tot].next=head[A]; 
    e[tot].w=w; head[A]=tot;
}
void init(){
    memset(e,-1,sizeof(e)); memset(head,0,sizeof(head));	
    memset(pre,0,sizeof(pre)); memset(inq,0,sizeof(inq));
    memset(cnt,0,sizeof(cnt)); memset(noPath,false,sizeof(noPath));
    while(q.size()) q.pop(); tot=0;
}
void dfs(int u){
    for(int i=head[u];i;i=e[i].next) {
    	if(!noPath[e[i].to]){
    	    noPath[e[i].to]=true; dfs(e[i].to);
    	}
    }
}
void get_sum_of_Weight(int s){
    _for(i,1,N+1) dis[i]=INF;
    dis[s]=0; inq[s]=1; q.push(s);
    while(!q.empty()){
    	int u=q.front();q.pop();  inq[u]=0;
    	for(int i=head[u];i;i=e[i].next){
    	   int v=e[i].to;
           if(dis[v]>dis[u]+e[i].w){
    	       cnt[v]=cnt[u]+1;
    	       if(cnt[v]>=N){
     	       noPath[v]=true; dfs(v); continue;
    	       }
    	      dis[v]=dis[u]+e[i].w; 
    	      pre[v]=u;
    	      if(!inq[v]){
    	      q.push(v); inq[v]=1;
    	      }	
          }
       }
  }
}
void output(int P){
    if(dis[P]&lt;3 || dis[P]==INF || noPath[P]) printf("?\n");
    else printf("%d\n",dis[P]);
}
int main(){
    scanf("%d",&amp;T);
    int A,B,w;
    _for(j,0,T){
        init(); scanf("%d",&amp;N);
    	_for(i,1,N+1)  scanf("%d",&amp;W[i]); 
    	scanf("%d",&amp;M);
    	_for(i,0,M){
    	    scanf("%d%d",&amp;A,&amp;B);
    	    w=pow(W[B]-W[A],3);
    	    addedge(A,B,w);
    	}
    	get_sum_of_Weight(1);
    	scanf("%d",&amp;Q);
    	printf("Case %d:\n",j+1);
    	_for(i,0,Q){
    	    scanf("%d",&amp;P); output(P);
    	}
    }
    return 0;
}</code></pre>
<!-- /wp:code -->
# 结束       &nbsp;    [返回首页](./index.md)&nbsp;  [下篇 CSP-M2](./CSP-M2.md)
