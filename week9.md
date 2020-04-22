<!-- wp:heading -->
<h2 id="problem-title">A - 咕咕东的目录管理器</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 id="题面">Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>咕咕东的雪梨电脑的操作系统在上个月受到宇宙射线的影响，时不时发生故障，他受不了了，想要写一个高效易用零bug的操作系统 —— 这工程量太大了，所以他定了一个小目标，从实现一个目录管理器开始。前些日子，东东的电脑终于因为过度收到宇宙射线的影响而宕机，无法写代码。他的好友TT正忙着在B站看猫片，另一位好友瑞神正忙着打守望先锋。现在只有你能帮助东东！</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>初始时，咕咕东的硬盘是空的，命令行的当前目录为根目录&nbsp;<code>root</code>。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>目录管理器可以理解为要维护一棵有根树结构，每个目录的儿子必须保持字典序。</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://s1.ax1x.com/2020/04/10/GojFbt.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>现在咕咕东可以在命令行下执行以下表格中描述的命令：</p>
<!-- /wp:paragraph -->

<!-- wp:table -->
<table class="wp-block-table"><thead><tr><th>命令</th><th>类型</th><th>实现</th><th>说明</th></tr></thead><tbody><tr><td>MKDIR&nbsp;<em>s</em></td><td>操作</td><td>在当前目录下创建一个子目录&nbsp;<em>s</em>，<em>s</em>&nbsp;是一个字符串</td><td>创建成功输出 "OK"；若当前目录下已有该子目录则输出 "ERR"</td></tr><tr><td>RM&nbsp;<em>s</em></td><td>操作</td><td>在当前目录下删除子目录&nbsp;<em>s</em>，<em>s</em>&nbsp;是一个字符串</td><td>删除成功输出 "OK"；若当前目录下该子目录不存在则输出 "ERR"</td></tr><tr><td>CD&nbsp;<em>s</em></td><td>操作</td><td>进入一个子目录 s，<em>s</em>&nbsp;是一个字符串（执行后，当前目录可能会改变）</td><td>进入成功输出 "OK"；若当前目录下该子目录不存在则输出 "ERR"<br>特殊地，若&nbsp;<em>s</em>&nbsp;等于 ".." 则表示返回上级目录，同理，返回成功输出 “OK”，返回失败（当前目录已是根目录没有上级目录）则输出 “ERR”</td></tr><tr><td>SZ</td><td>询问</td><td>输出当前目录的大小</td><td>也即输出 1+当前目录的子目录数</td></tr><tr><td>LS</td><td>询问</td><td>输出多行表示当前目录的 "直接子目录" 名</td><td>若没有子目录，则输出 "EMPTY"；若子目录数属于 [1,10] 则全部输出；若子目录数大于 10，则输出前 5 个，再输出一行 "…"，输出后 5 个。</td></tr><tr><td>TREE</td><td>询问</td><td>输出多行表示以当前目录为根的子树的前序遍历结果</td><td>若没有后代目录，则输出 "EMPTY"；若后代目录数+1（当前目录）属于 [1,10] 则全部输出；若后代目录数+1（当前目录）大于 10，则输出前 5 个，再输出一行 "…"，输出后 5 个。若目录结构如上图，当前目录为 "root" 执行结果如下，</td></tr><tr><td>UNDO</td><td>特殊</td><td>撤销操作</td><td>撤销最近一个 "成功执行" 的操作（即MKDIR或RM或CD）的影响</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3 id="输入"> Input </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>输入文件包含多组测试数据，第一行输入一个整数表示测试数据的组数 T （T &lt;= 20）；</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>每组测试数据的第一行输入一个整数表示该组测试数据的命令总数 Q （Q &lt;= 1e5）；</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>每组测试数据的 2 ~ Q+1 行为具体的操作 （MKDIR、RM 操作总数不超过 5000）；</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="面对数据范围你要思考的是他们代表的-命令-执行的最大可接受复杂度，只有这样你才能知道你需要设计的是怎样复杂度的系统。">面对数据范围你要思考的是他们代表的 "命令" 执行的最大可接受复杂度，只有这样你才能知道你需要设计的是怎样复杂度的系统。</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 id="输出"> Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>每组测试数据的输出结果间需要输出一行空行。注意大小写敏感。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="时空限制">Note</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Time limit 6000 ms</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Memory limit 1048576 kB</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="样例输入">Input Example  </h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>1
22
MKDIR dira
CD dirb
CD dira
MKDIR a
MKDIR b
MKDIR c
CD ..
MKDIR dirb
CD dirb
MKDIR x
CD ..
MKDIR dirc
CD dirc
MKDIR y
CD ..
SZ
LS
TREE
RM dira
TREE
UNDO
TREE</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3 id="样例输出"> Output Example  </h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>OK
ERR
OK
OK
OK
OK
OK
OK
OK
OK
OK
OK
OK
OK
OK
9
dira
dirb
dirc
root
dira
a
b
c
dirb
x
dirc
y
OK
root
dirb
x
dirc
y
OK
root
dira
a
b
c
dirb
x
dirc
y</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>利用map结构来储存每个目录节点的对应子目录，节点的关键字用数组的下标来表示。对于撤销功能，可以用容器vector储存，每次mkdir,rm,cd命令成功后，都把其对应的命令、当前目录、操作的子目录信息存下来。由于可能多次遇到同一目录的打印，可以先根据当前子目录数量把可能要打印到的都保存下来，如果打印时这些信息没有改动就可以直接打印，如果遇到其他操作改动就重新更新下之前保存的信息。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std; 
const int maxn=1e5+10;
const string str[]={"MKDIR","RM","CD","SZ","LS","TREE","UNDO"};
int tot,n,t;
struct CMD{
	string name,tr;
	int type;
	void init(string s){
		name=s;
		for(int i=0;i&lt;7;++i){
			if(s==str[i]){
				type=i; if(i&lt;3) cin>>tr; break;
			}
		}
	}
}cmd;
struct Node{
	string name;
	map&lt;string,int> nexts;
	int root,sz;
	vector&lt;string> Front,End;//保存前面几个，保存后面几个 
	bool updated;
	void init(string s,int rt){
		updated=false; root=rt;
		name=s; sz=1;
		Front.clear(); End.clear();
	    nexts.clear();
	} 
}node[maxn];
class Tree{
	protected:
	int now;//实时位置
	int tot;	
	Node root;
	vector&lt;pair&lt;string,pair&lt;int,int> > > undo;
	CMD cmd;
	public:
	  void init(){
	  	node[0].init("root",-1); root=node[0];
		undo.clear(); tot=0; now=0;
	  }
	  void add(string s,int rt){
	  	node[++tot].init(s,rt);
	  	node[rt].nexts[s]=tot;
	  }
	  void update(int id,int num){
	    while(id!=-1) {
	  		node[id].updated=0;
	  		node[id].sz+=num;
	  		id = node[id].root;
		  }
	  }
	  void MKDIR(){
	   if(node[now].nexts.count(cmd.tr)){
	   	cout&lt;&lt;"ERR"&lt;&lt;endl;
	   	return;
	   }
	   add(cmd.tr,now);
	   update(now,1);
	   undo.push_back(make_pair("MKDIR",make_pair(now,tot)));
	   cout&lt;&lt;"OK"&lt;&lt;endl;	   
	  }
	  void RM(){
	  	if(!node[now].nexts.count(cmd.tr)){
	   	cout&lt;&lt;"ERR"&lt;&lt;endl;
	   	return;
	   }
	   int u=node[now].nexts[cmd.tr];
	   update(now,(-1)*node[u].sz);
	   node[now].nexts.erase(node[u].name);
	   undo.push_back(make_pair("RM",make_pair(now,u)));
	   cout&lt;&lt;"OK"&lt;&lt;endl;
	  }
	  void CD(){
	  	if(cmd.tr==".."){
	  		if(node[now].root==-1){
	  			cout&lt;&lt;"ERR"&lt;&lt;endl;return;
			  }
			undo.push_back(make_pair("CD",make_pair(now,node[now].root)));
			now =node[now].root;
			cout&lt;&lt;"OK"&lt;&lt;endl;return;
		  }
		if(!node[now].nexts.count(cmd.tr)){
			cout&lt;&lt;"ERR"&lt;&lt;endl;return;
		}
		int u=node[now].nexts[cmd.tr];
		undo.push_back(make_pair("CD",make_pair(now,u)));
		now=u;
		cout&lt;&lt;"OK"&lt;&lt;endl;
	  } 
	  void SZ(){ cout&lt;&lt;node[now].sz&lt;&lt;endl; }
	  void LS(){
	  	int t=node[now].nexts.size();
		if(t==0){
			cout&lt;&lt;"EMPTY"&lt;&lt;endl;return;
		} 
		auto pos=node[now].nexts.begin();
		if(t > 0 &amp;&amp; t &lt; 11){
			while(pos!=node[now].nexts.end()){
				cout&lt;&lt;pos->first&lt;&lt;endl;pos++;
			}return;
		}
		for(int i=0;i&lt;5;++i){
			cout&lt;&lt;pos->first&lt;&lt;endl; pos++;
		}
		cout&lt;&lt;"..."&lt;&lt;endl;
		pos=node[now].nexts.end();
		for(int i=0;i&lt;5;++i) pos--;
		for(int i=0;i&lt;5;++i){
			cout&lt;&lt;pos->first&lt;&lt;endl; pos++;	
		}
	  }
	  void viewFront(int id){
	  	node[id].Front.push_back(node[id].name);
	  	if(node[id].sz==1) return ;
	  	if(node[id].sz&lt;11) {
	  		for(auto i:node[id].nexts){
	  			if(!node[i.second].updated) push(i.second);
	  			node[id].Front.insert(node[id].Front.end(),node[i.second].Front.begin(),node[i.second].Front.end());
			  }
			return;
		  }
		int ct=1;
		for(auto i:node[id].nexts){
		   if(!node[i.second].updated) push(i.second);
		   for(auto j:node[i.second].Front){
		   	node[id].Front.push_back(j);
		   	++ct;
		   	if(ct>=5) break;
		   }
		   if(ct>=5) break;
		}
	  }
	  void viewEnd(int id){
	  	int ct=0;
	  	auto it=node[id].nexts.end();
	  	--it;
	  	for(;;--it){
	  		if(!node[it->second].updated) push(it->second);
			int u=it->second;
			for(int i=node[u].End.size()-1;i>=0;--i){
				node[id].End.push_back(node[u].End[i]);
				++ct;
				if(ct>=5){
					reverse(node[id].End.begin(),node[id].End.end());
					break;
				}	
			} 
			if(ct>=5) break; 
			if(it==node[id].nexts.begin()) break;
		  }
	  }
	  void push(int id){
      node[id].Front.clear(); node[id].End.clear();
      viewFront(id);
      if(node[id].sz>10) viewEnd(id);
      else node[id].End=node[id].Front;
      node[id].updated=true;
	}
	  void TREE(){
	  	if(!node[now].updated) push(now);
	  	if(node[now].sz==1) cout&lt;&lt;"EMPTY"&lt;&lt;endl;
	  	else if(node[now].sz>1 &amp;&amp;node[now].sz&lt;11){
	  		for(int i=0;i&lt;node[now].Front.size();++i) cout&lt;&lt;node[now].Front[i]&lt;&lt;endl;
		  }
		else{
			for(int i=0;i&lt;5;++i) cout&lt;&lt;node[now].Front[i]&lt;&lt;endl;
			cout&lt;&lt;"..."&lt;&lt;endl;
			for(int i=5;i>0;--i) cout&lt;&lt;node[now].End[node[now].End.size()-i]&lt;&lt;endl;
		}
	  }
      void UNDO(){
      	if(!undo.size()){
      		cout&lt;&lt;"ERR"&lt;&lt;endl;return;
		  }
		auto e= undo[undo.size()-1];
		undo.pop_back();
		cout&lt;&lt;"OK"&lt;&lt;endl;
		int tmp=now;
		if(e.first=="MKDIR"){
			cmd.name="RM";
			now = e.second.first;
			cmd.tr=node[e.second.second].name;
			int u= node[now].nexts[cmd.tr];
			update(now,(-1)*node[u].sz);
			node[now].nexts.erase(node[u].name);
			now=tmp;
		}
		else if(e.first=="RM"){
			now = e.second.first;
			int u=e.second.second;
			update(now,node[u].sz);
			node[now].nexts[node[u].name]=u;
			now=tmp;
		}
		else{
			now=e.second.first;
		}
	  }
	  void SOLVE(){
	  	init();
	  	for(int i=0;i&lt;n;++i){
	  		string s; cin>>s;  cmd.init(s);
	  		switch(cmd.type){
	  			case 0: MKDIR();break;
	  			case 1: RM();break;
	  			case 2: CD();break;
	  			case 3: SZ();break;
	  			case 4: LS();break;
	  			case 5: TREE();break;
	  			case 6:	UNDO();break;
			  }
		  }
	  }
}tree; 
int main(){ 
    ios::sync_with_stdio(false); 
    cin>>t;
    for(int i=0;i&lt;t;++i){
    	cin>>n;
		tree.SOLVE();
	}
    return 0;
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2 id="problem-title">B - 东东学打牌</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 id="题面"> Description  </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>最近，东东沉迷于打牌。所以他找到 HRZ、ZJM 等人和他一起打牌。由于人数众多，东东稍微修改了亿下游戏规则：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>所有扑克牌只按数字来算大小，忽略花色。</li><li>每张扑克牌的大小由一个值表示。A, 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K 分别指代 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13。</li><li>每个玩家抽得 5 张扑克牌，组成一手牌！（每种扑克牌的张数是无限的，你不用担心，东东家里有无数副扑克牌）</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>理所当然地，一手牌是有不同类型，并且有大小之分的。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>举个栗子，现在东东的 "一手牌"（记为 α），瑞神的 "一手牌"（记为 β），要么 α &gt; β，要么 α &lt; β，要么 α = β。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>那么这两个 "一手牌"，如何进行比较大小呢？首先对于不同类型的一手牌，其值的大小即下面的标号；对于同类型的一手牌，根据组成这手牌的 5 张牌不同，其值不同。下面依次列举了这手牌的形成规则：</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>大牌：这手牌不符合下面任一个形成规则。如果 α 和 β 都是大牌，那么定义它们的大小为组成这手牌的 5 张牌的大小总和。</li><li>对子：5 张牌中有 2 张牌的值相等。如果 α 和 β 都是对子，比较这个 "对子" 的大小，如果 α 和 β 的 "对子" 大小相等，那么比较剩下 3 张牌的总和。</li><li>两对：5 张牌中有两个不同的对子。如果 α 和 β 都是两对，先比较双方较大的那个对子，如果相等，再比较双方较小的那个对子，如果还相等，只能比较 5 张牌中的最后那张牌组不成对子的牌。</li><li>三个：5 张牌中有 3 张牌的值相等。如果 α 和 β 都是 "三个"，比较这个 "三个" 的大小，如果 α 和 β 的 "三个" 大小相等，那么比较剩下 2 张牌的总和。</li><li>三带二：5 张牌中有 3 张牌的值相等，另外 2 张牌值也相等。如果 α 和 β 都是 "三带二"，先比较它们的 "三个" 的大小，如果相等，再比较 "对子" 的大小。</li><li>炸弹：5 张牌中有 4 张牌的值相等。如果 α 和 β 都是 "炸弹"，比较 "炸弹" 的大小，如果相等，比较剩下那张牌的大小。</li><li>顺子：5 张牌中形成 x, x+1, x+2, x+3, x+4。如果 α 和 β 都是 "顺子"，直接比较两个顺子的最大值。</li><li>龙顺子：5 张牌分别为 10、J、Q、K、A。</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>作为一个称职的魔法师，东东得知了全场人手里 5 张牌的情况。他现在要输出一个排行榜。排行榜按照选手们的 "一手牌" 大小进行排序，如果两个选手的牌相等，那么人名字典序小的排在前面。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>不料，此时一束宇宙射线扫过，为了躲避宇宙射线，东东慌乱中清空了他脑中的 Cache。请你告诉东东，全场人的排名</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="输入"> Input </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>输入包含多组数据。每组输入开头一个整数 n (1 &lt;= n &lt;= 1e5)，表明全场共多少人。<br>随后是 n 行，每行一个字符串 s1 和 s2 （1 &lt;= |s1|,|s2| &lt;= 10）， s1 是对应人的名字，s2 是他手里的牌情况。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="输出"> Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对于每组测试数据，输出 n 行，即这次全场人的排名。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Input Example </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>3<br>DongDong AAA109<br>ZJM 678910<br>Hrz 678910</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output Example </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Hrz<br>ZJM<br>DongDong</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
```
大致步骤分: 
1.区分出每个人的牌型  
2.重定义比较方法  
3.排序
4.打印
```

<!-- wp:paragraph -->
<p>设出牌型可能需要用到的变量，比如存在2个数一样的数key2_1,如果还存在第二个就设为key2_2,同理，如果遇到存在重复三次出现就赋给key3,如果key2_2存在就将其赋给key3_2。当然更新这些变量时候也需要注意把它原来的变量置为0，比如把key2_1给了key3就要把key2_1=0,把key3给了key4时需要把key3再置为0···之后我们就可以通过判断这些变量的存在(>0)来确定牌型，同时把所有变量都加入到card节点中，之后在card中根据牌型和这些变量来重定义大小关系。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
const int maxn=1e5 + 5;
int n;int cd[15];int tot=0;
struct card{
	string name;
	int sum,key;//五张之和,类型 
	int key2_1,key2_2,key3,key3_2,key4;
	bool operator&lt;(card p){
		if(key!=p.key) return key > p.key;//牌型比较 
		else{
			switch(key){
				case 8: case 1: case 7: if(sum!=p.sum) return sum > p.sum; else return name &lt; p.name;
				case 2: if(key2_1 != p.key2_1) return key2_1 > p.key2_1;  else{ if(sum!=p.sum) return sum > p.sum;  else return name &lt; p.name; }
				case 3: if(key2_1 != p.key2_1) return key2_1 > p.key2_1;
		  	            else {
		  		          if(key2_2 != p.key2_2) return key2_2 > p.key2_2;
		  		          else{ if(sum!=p.sum) return sum > p.sum;  else return name &lt; p.name; }
			            }
				case 4: if(key3!=p.key3) return key3 > p.key3; else{ if(sum!=p.sum) return sum > p.sum;  else return name &lt; p.name; }
				case 5: if(key3!=p.key3) return key3 > p.key3; 	else{ if(key3_2!=p.key3_2) return key3_2 > p.key3_2; else return name&lt;p.name; }
				case 6:	if(key4!=p.key4) return key4 > p.key4;  else{ if(sum!=p.sum) return sum > p.sum;  else return name&lt;p.name; }
			} 
	     }
    }
}cards[maxn];
void add(string name,string str){
	card p; memset(cd,0,sizeof(cd));
	int size=str.size(); int t; int sum=0,key=1,key2_1=0,key2_2=0,key3=0,key3_2=0,key4=0; int max=-1,min=15;
	for(int i=0;i&lt;size;++i){
		t=0; switch(str[i]){
			case '0': t=0;break;
			case '1': t=10;++cd[t]; break;
			case 'A': t=1;++cd[t];  break;
			case 'J': t=11;++cd[t]; break;
			case 'Q': t=12;++cd[t]; break;
			case 'K': t=13;++cd[t]; break;		
			default: t=str[i]-'0'; ++cd[t];break;//2~9
		}   sum+=t;
		if(t){
		 switch(cd[t]){
		  case 2: if(key2_1) key2_2=t; else key2_1=t; break;
		  case 3: if(key2_1==t) { key2_1=0;key3=t; }
		          else  { key2_2=0;key3=t; } break;//后面记得如果出现2时把其置为key3_2  
		  case 4: key3=0;key4=t; break;
		 }
		 if(t>max) max=t; if(t&lt;min) min=t;
		}
	}  
	if(key4) key=6;
	else if(key3){
		key3_2=(key2_1==0)?key2_2:key2_1;
		if(key3_2) { key2_1=key2_2=0; key=5; } else key=4;
	}
	else if( key2_1 || key2_2 ){
	  if(key2_1 &amp;&amp; key2_2){
	  	key=3; if(key2_1 &lt; key2_2) swap(key2_1,key2_2);
	  }	
	  else { key2_1= key2_1>0 ? key2_1: key2_2; key=2; }
	}
	else if((max-min)==4) { key=7; }
	else if(cd[1] &amp;&amp; cd[10] &amp;&amp; cd[11] &amp;&amp; cd[12] &amp;&amp; cd[13]) { key=8; }
	else key=1;
	p.key=key; p.key2_1=key2_1;p.key2_2=key2_2; p.key3=key3; p.key3_2=key3_2; p.key4=key4; p.name=name; p.sum=sum;
	cards[tot]=p; ++tot;
}
void output(){
	for(int i=0;i&lt;tot;++i) cout&lt;&lt;cards[i].name&lt;&lt;endl;
}
int main(){
	string s1,s2; 
	while(~scanf("%d",&amp;n)){
	  tot=0;
	  while(n--){
	    cin>>s1>>s2; add(s1,s2);
	  } 
	  sort(cards,cards+tot); output();
	}
	return 0;
} </code></pre>
<!-- /wp:code -->

<!-- wp:heading -->
<h2 id="problem-title">C - 签到题，独立思考哈</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Description </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>SDUQD 旁边的滨海公园有 x 条长凳。第 i 个长凳上坐着 a_i 个人。这时候又有 y 个人将来到公园，他们将选择坐在某些公园中的长凳上，那么当这 y 个人坐下后，记k = 所有椅子上的人数的最大值，那么k可能的最大值mx和最小值mn分别是多少。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Input </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>第一行包含一个整数 x (1 &lt;= x &lt;= 100) 表示公园中长椅的数目<br>第二行包含一个整数 y (1 &lt;= y &lt;= 1000) 表示有 y 个人来到公园<br>接下来 x 个整数 a_i (1&lt;=a_i&lt;=100)，表示初始时公园长椅上坐着的人数Output</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> mn 和 mx</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Input Example </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>3<br>7<br>1<br>6<br>1</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3> Output Example </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>6 13</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Note</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>最初三张椅子的人数分别为 1 6 1<br>接下来来了7个人。<br>可能出现的情况为{1 6 8},{1,7,7},…,{8,6,1}<br>相对应的k分别为8,7,…,8<br>其中，状态{1,13,1}的k = 13，为mx<br>状态{4,6,5}和状态{5,6,4}的k = 6，为mn</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:preformatted -->
```
设原先的最大人数为maxn.最大值好判断，就是把所有人都分给原先最多的椅子,即maxn+y。
最大人数的最小值，设其他人与maxn的差值之和为sumn，如果y&lt;sumn，说明最大人数的最小值一定在maxn椅子处，不可能存在更小的最大值.
如果y>sumn，那也就是即便先把人给其他椅子差值填满之后，还有多余的人，不管加给谁，最大值都会比maxn大。
剩下的人先均分，当不能均分的时候，也就是说不会更小了，如果恰好够分此时存在最大值的最小值;如果存在余数,最大值+1。
即 Min=maxn+(y-sumn)/x , Min+=((y-sumn)%x)?0:1;
```
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;bits/stdc++.h>
using namespace std;
int x,y;
int a[101];
int main(){
	int maxn=-1,sumn=0,Max,Min;
	cin >> x >> y;
	for(int i=0;i&lt;x;++i){
	 cin>>a[i]; sumn+=a[i]; 
	 if(a[i]>maxn) maxn=a[i];	
	} 
	Max=maxn+y; sumn=x*maxn-sumn; 
	if(y&lt;=sumn) Min=maxn;
	else{
		Min=maxn+ (y-sumn)/x;
		if((y-sumn)%x) Min+=1;
	}
	cout&lt;&lt;Min&lt;&lt;" "&lt;&lt;Max;
	return 0;
} </code></pre>
<!-- /wp:code -->
