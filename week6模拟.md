# 程序设计思维与实践 第六周 限时大模拟           &nbsp;    [返回首页](./index.md)&nbsp;  [上篇 Week5](./week5.md)
<!-- wp:heading {"level":3} -->
<h3>Description</h3>
<!-- /wp:heading -->

<!-- wp:paragraph {"customFontSize":16} -->
<p style="font-size:16px">从瑞神家打牌回来后，东东痛定思痛，决定苦练牌技，终成赌神！<br>东东有&nbsp;<em style="user-select: auto;">A</em> × <em style="user-select: auto;">B</em>&nbsp;张扑克牌。每张扑克牌有一个大小(整数，记为a，范围区间是0到A-1）和一个花色（整数，记为b，范围区间是&nbsp;0&nbsp;到&nbsp;<em style="user-select: auto;">B</em> - 1。扑克牌是互异的，也就是独一无二的，也就是说没有两张牌大小和花色都相同。 “一手牌”的意思是你手里有5张不同的牌，这 5 张牌没有谁在前谁在后的顺序之分，它们可以形成一个牌型。 我们定义了 9 种牌型，如下是 9 种牌型的规则，我们用“低序号优先”来匹配牌型，即这“一手牌”从上到下满足的第一个牌型规则就是它的“牌型编号”（一个整数，属于1到9）：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>1.同花顺: 同时满足规则 2 和规则 3.</li><li>2.顺子 : 5张牌的大小形如&nbsp;<em style="user-select: auto;">x</em>,&nbsp;<em style="user-select: auto;">x</em> + 1,&nbsp;<em style="user-select: auto;">x</em> + 2,&nbsp;<em style="user-select: auto;">x</em> + 3,&nbsp;<em style="user-select: auto;">x</em> + 4</li><li>3.同花 : 5张牌都是相同花色的.</li><li>4.炸弹 : 5张牌其中有4张牌的大小相等.</li><li>5.三带二 : 5张牌其中有3张牌的大小相等，且另外2张牌的大小也相等.</li><li>6.两对: 5张牌其中有2张牌的大小相等，且另外3张牌中2张牌的大小相等.</li><li>7.三条: 5张牌其中有3张牌的大小相等.</li><li>8.一对: 5张牌其中有2张牌的大小相等.</li><li>9.要不起: 这手牌不满足上述的牌型中任意一个.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph {"customFontSize":15} -->
<p style="font-size:15px">现在, 东东从<em style="user-select: auto;">A</em> × <em style="user-select: auto;">B</em>&nbsp;张扑克牌中拿走了 2 张牌！分别是&nbsp;(<em style="user-select: auto;">a</em><sub style="user-select: auto;">1</sub>,&nbsp;<em style="user-select: auto;">b</em><sub style="user-select: auto;">1</sub>)&nbsp;和&nbsp;(<em style="user-select: auto;">a</em><sub style="user-select: auto;">2</sub>, <em style="user-select: auto;">b</em><sub style="user-select: auto;">2</sub>). （其中a表示大小，b表示花色）<br>现在要从剩下的扑克牌中再随机拿出 3 张！组成一手牌！！<br>其实东东除了会打代码，他业余还是一个魔法师，现在他要预言他的未来的可能性，即他将拿到的“一手牌”的可能性，我们用一个“牌型编号（一个整数，属于1到9）”来表示这手牌的牌型，那么他的未来有 9 种可能，但每种可能的方案数不一样。<br>现在，东东的阿戈摩托之眼没了，你需要帮他算一算 9 种牌型中，每种牌型的方案数。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"width":646,"height":334} -->
<figure class="wp-block-image is-resized"><img src="https://s1.ax1x.com/2020/03/25/8vIBsf.png" alt="" width="646" height="334"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>Input</h3>
<!-- /wp:heading -->

<!-- wp:paragraph {"customFontSize":15} -->
<p style="font-size:15px">第&nbsp;1&nbsp;行包含了整数&nbsp;<em>A</em>&nbsp;和&nbsp;<em>B</em>&nbsp;(5 ≤ <em>A</em> ≤ 25, 1 ≤ <em>B</em> ≤ 4).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"customFontSize":15} -->
<p style="font-size:15px">第&nbsp;2&nbsp;行包含了整数&nbsp;<em>a</em><sub>1</sub>,&nbsp;<em>b</em><sub>1</sub>,&nbsp;<em>a</em><sub>2</sub>,&nbsp;<em>b</em><sub>2</sub>&nbsp;(0 ≤ <em>a</em><sub>1</sub>, <em>a</em><sub>2</sub> ≤ <em>A</em> - 1, 0 ≤ <em>b</em><sub>1</sub>, <em>b</em><sub>2</sub> ≤ <em>B</em> - 1, (<em>a</em><sub>1</sub>, <em>b</em><sub>1</sub>) ≠ (<em>a</em><sub>2</sub>, <em>b</em><sub>2</sub>)).</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Output</h3>
<!-- /wp:heading -->

<!-- wp:paragraph {"customFontSize":15} -->
<p style="font-size:15px">

输出一行，这行有 9 个整数，每个整数代表了 9 种牌型的方案数（按牌型编号从小到大的顺序）

</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Examples</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">5 2
1 0 3 1 </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">0 8 0 0 0 12 0 36 0</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Input</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">25 4
0 0 24 3</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":4} -->
<h4>Output</h4>
<!-- /wp:heading -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">0 0 0 2 18 1656 644 36432 113344</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->
<h3>Idea</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>这道模拟题需要分情况处理，另外通过增加每个情况的可能出现的先决条件来剔除一些不会出现的可能，减少运算负担。比如如果已经抽好的两张牌本身就不同色或者差值&gt;=5或者相等，同花顺情况都一定为0。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>其中不同情况的判断和处理如下:(考虑的都是从已知的A,B,a1,a2,b1,b2判断后可以出现该种情况的条件下)</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":44} -->
<figure class="wp-block-image"><img src="https://www.xupengbo.cn/wp-content/uploads/2020/03/image-5-1024x586.png" alt="" class="wp-image-44"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Codes</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#include&lt;iostream>
#include&lt;algorithm>
using namespace std;
int A,B,a1,b1,a2,b2;
int S[9]={0}; //存放最终结果 
void getChance1239(){
	int dis=abs(a1-a2); int cnt=0;
	if(dis&lt;5 &amp;&amp; dis>0){
	 for(int i=0;i&lt;A-4;++i) 
		if(i&lt;=a1 &amp;&amp; i&lt;=a2 &amp;&amp; a1&lt;=i+4 &amp;&amp; a2&lt;=i+4) 	++cnt;   
	 if(b1==b2) S[0]=cnt; 
	 S[1]=cnt*B*B*B;  
	}  
	if(b1==b2) 
		S[2]=(A-2)*(A-3)*(A-4)/6;  
	S[1] -= S[0];
	S[2] -= S[0];
	if(a1!=a2)
	S[8]=(A-2)*(A-3)*(A-4)*B*B*B/6 -(S[0]+S[1]+S[2]);
}
void getChance4(){//四张牌都一样的大小 
	if(B==4){
	  if(a1!=a2) S[3]=2;
	  else S[3]=A-1;
	}  
}
void getChance5(){
	if(B>2){
	if(a1==a2) 
		S[4]=(A-1)*(B*(B-1)*(B-2)/2 + B*(B-1)*(B-2)/6); 
	else 
		S[4]=(B-1)*(B-2)*(B-1); 
	}
}
void getChance6(){
	if(B>1){
	  if(a1==a2) 
		S[5]=(A-1)*(A-2)*B*B*(B-1)/2; 
	  else 
		S[5]=(A-2)*B*(B-1)*(B-1)*2; 
	}
}
void getChance7(){
	if(B>2) { 	
     if(a1==a2) 
	   S[6]=(B-2)*(A-1)*(A-2)*B*B/2; 
	 else 
	   S[6]=B*(B-1)*(B-2)*(A-2) + (A-2)*B*(B-1)*(B-2)/6; 
	}
}
void getChance8(){
	if(B>1){
 	  if(a1==a2)
	    S[7]=B*B*B*(A-1)*(A-2)*(A-3)/6;	
	  else
	    S[7]=(B-1)*(A-2)*(A-3)*B*B + B*(A-3)*(A-2)*B*(B-1)/2;
	}
} 
void getChance(){  
	getChance1239(); //1 2 3 9放一起 
	getChance4(); getChance5(); getChance6();
	getChance7(); getChance8();
}
void input(){
	scanf("%d%d",&amp;A,&amp;B);
	scanf("%d%d%d%d",&amp;a1,&amp;b1,&amp;a2,&amp;b2);
}
void output(){
	for(int i=0;i&lt;9;i++)
	  printf("%d ",S[i]);
}
int main(){
	input();
	getChance();
	output();
	return 0;
}</code></pre>
<!-- /wp:code -->
# 结束！    &nbsp;&nbsp;&nbsp;    [返回首页](./index.md)&nbsp;&nbsp;  [下篇 week6作业](./week6.md)
