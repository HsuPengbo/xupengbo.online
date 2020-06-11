# 程序设计思维与实践 第14周 作业+限时模拟    [返回首页](./index.md)        [上篇 元素选择器](./CSP-201809-3.md)
# 作业第3题 Q老师的考验(选做题未做)
## Description
Lele now is thinking about a simple function f(x).

If x < 10 f(x) = x.
If x >= 10 f(x) = a0 * f(x-1) + a1 * f(x-2) + a2 * f(x-3) + …… + a9 * f(x-10);
And ai(0<=i<=9) can only be 0 or 1 .

Now, I will give a0 ~ a9 and two positive integers k and m ,and could you help Lele to caculate f(k)%m.
## Input

The problem contains mutiple test cases.Please process to the end of file.
In each case, there will be two lines.
In the first line , there are two positive integers k and m. ( k<2*10^9 , m < 10^5 )
In the second line , there are ten integers represent a0 ~ a9.
## Output

For each case, output f(k) % m in one line.
## Sample Input
```
10 9999
1 1 1 1 1 1 1 1 1 1
20 500
1 0 1 0 1 0 1 0 1 0
```
## Sample Output
```
45
104
```
## Idea
这道题属于矩阵快速幂的简单应用。题目给定的线性递推式很长，但是并不难，当 x ≥ 10 时，f(x) = a0 * f(x-1) + a1 * f(x-2) + a2 * f(x-3) + …… + a9 * f(x-10)。 
![](https://blog.xupengbo.online/images/2020061101.png?raw=true)
## Codes
```
#include<cstdio>
#include<cstring>
int a[10],k,m,ans;
const int N=10;
struct Matrix{
	int x[N][N];
	Matrix operator*(const Matrix& t) const {
		Matrix ret;
		for(int i=0;i<N;++i){
			for(int j=0;j<N;++j){
				ret.x[i][j]=0;
				for(int k=0;k<N;++k){
					ret.x[i][j] += x[i][k]*t.x[k][j];
					ret.x[i][j] %=m;
				}
			}
		}
		return ret;
	}
	void Init(){ memset(x,0,sizeof(x)); }
	Matrix(){ memset(x,0,sizeof(x)); }
	Matrix(const Matrix& t) { memcpy(x,t.x,sizeof(x)); }
}; 
Matrix quick_pow(Matrix t,int x){
	Matrix ret;
	ret.Init();
	for(int i=0;i<N;++i)
		ret.x[i][i]=1;
	while(x){
		if(x&1) ret=ret*t;
		t=t*t;
		x>>=1;
	}
	return ret;
}
void solve(){
	if(k<10) {
	printf("%d\n",k%m);	return;
	}
	Matrix t;
	for(int i=0;i<N;++i) 
		t.x[0][i]=a[i]; 
	for(int i=1;i<N;++i) 
		t.x[i][i-1]=1;
	Matrix z=quick_pow(t,k-9);
	int ans=0;
	for(int i=0;i<N;++i){
		ans+= z.x[0][i]*(9-i);ans%=m;
	}
	printf("%d\n",ans);
}
int main(){
	while(~scanf("%d%d",&k,&m)){
		for(int i=0;i<10;++i) scanf("%d",&a[i]);
		solve();
	}
	return 0;
}
```


# 限时模拟
## Problem Cat [HDU-3700](http://acm.hdu.edu.cn/showproblem.php?pid=3700)
## Description
There is a cat, cat likes to sleep.
If he sleeps, he sleeps continuously no less than A hours.
For some strange reason, the cat can not stay awake continuously more than B hours.
The cat is lazy, it could sleep all the time,
but sometimes interesting events occur(such as cat food, TV show, etc) .
The cat loves these events very much.
So, Please help the cat plan their day so as not to miss any interesting events.
Every day the cat wants to live on the same schedule.
 

## Input
The first line of the input file contains two integers A and B (1 <= A, B <= 24).
The second line of the input file contains the number n, the number of interesting events (1 <= n <= 20).
Following n rows describe the interesting events.
Each event is described line of the form hh:mm-hh:mm, which specifies
the time period during which it occurs. Time varies from 00:00 to 23:59.
No two interesting events will overlap.
If the event is completed earlier than the beginning, This means that it captures midnight.
The event is considered to be occupying the whole minute,
when it begins and the moment when it ends (event 12:00-13:59 lasted exactly 120 minutes). Start time and time end of the event are different.
 

## Output
If the cat can organize their day so that during all the interesting events not sleep, print to output file Yes.

On the second line Bring k - how many times a day cat should go to bed.
In the following k rows Bring out the intervals in which the cat sleeps in the same format, in which interesting events are set in the input file. If making a few, display any.

If the cat can not organize their day desired way, print to the output file No.
 

## Sample Input

```
12 12
1
23:00-01:00
3 4
3
07:00-08:00
11:00-11:09
19:00-19:59
```

## Sample Output

```
Yes
1
01:07-22:13
No
```

## Idea
分析题意,每天的时间段不是睡觉,就是活动.睡觉时间段有下限,活动时间段有上限。由于给定的时间段必须是醒着的,所以我们可以判断,睡觉的时间段必然分布在醒着的时间段之间的区域。```(输入时如果出现了时间段Wakes[i].R>Wakes[i].L,记得Wakes[i].R+=T)```
由于每天是一个循环,所以当我们将一天必须活动时间段排序后,可以在当天最晚活动时间段Wakes[N-1]后面再加上一个时间段Wakes[N],有Wakes[N]=Wakes[0]+24h。这样就解决了跨夜问题。
从第一个空闲区间开始循环,如果满足>=A,就加入睡觉的时间段数组。
在睡觉数组后面加上第一个睡觉段(数组大小不用变化)，然后从第一个睡觉数组的末端开始检验每个相隔区间是否都<=B满足活动条件。最后根据之前的标记判断是否存在，存在输出Yes和Sleeps数组。
过程如下:

```
Input
Wakes[0]  Wakes[1] ... Wakes[N-1]    (Wakes[N]=Wakes[0]+24h)
检验Wakes[i].R~Wakes[i+1].L是否>=A
Sleeps[0] Sleeps[1] ... Sleeps[tot-1] (Sleeps[tot]=Sleeps[0]+24h)
检验Sleeps[i].R ~ Sleeps[i+1].L 是否<=B 
Output
```

## Codes

```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
int A, B, N, tot; char str[20];
const int T = 1440;
struct Node {
	int L, R;
	bool operator<(Node p) { return L < p.L; }
}Wakes[21], Sleeps[21];
void inttotime(int i) {
	int T1 = Sleeps[i].L, T2 = Sleeps[i].R;
	T1 %= T; T2 %= T;
	printf("%02d:%02d-%02d:%02d\n", T1 / 60, T1 % 60, T2 / 60, T2 % 60);
}
void timetoint(int i) {
	Wakes[i].L = (str[0] - '0') * 600 + (str[1] - '0') * 60 + (str[3] - '0') * 10 + (str[4] - '0');
	Wakes[i].R = (str[6] - '0') * 600 + (str[7] - '0') * 60 + (str[9] - '0') * 10 + (str[10] - '0');
	if (Wakes[i].R < Wakes[i].L) Wakes[i].R += T;
}
int main() {
	while (~scanf("%d %d", &A, &B)) {
		scanf("%d", &N);
		tot = 0; A *= 60; B *= 60;
		int l, r, i;
		for (i = 0; i < N; ++i) {
			scanf("%s", str); timetoint(i);
		}
		bool failed = false;
		sort(Wakes, Wakes + N);
		Wakes[N].L = Wakes[0].L + T;
		Wakes[N].R = Wakes[0].R + T;
		for (i = 0; i < N; ++i) {
			l = Wakes[i].R + 1;
			r = Wakes[i + 1].L - 1 ;
			if (r - l + 1 >= A) {
				Sleeps[tot].L = l;
				Sleeps[tot++].R = r;
			}
		}
		if (tot == 0) failed = true;
		Sleeps[tot].L = Sleeps[0].L + T;
		Sleeps[tot].R = Sleeps[0].R + T;
		for (i = 0; i < tot; ++i) {
			l = Sleeps[i].R + 1;
			r = Sleeps[i + 1].L - 1;
			if (r - l + 1 > B) { failed = true;	break; }
		}
		if (failed) { printf("No\n"); continue; } 
		printf("Yes\n%d\n", tot);
		for (i = 0; i < tot; ++i) {
			inttotime(i);
		}
	}
	return 0;
}
```
				    
# 结束!       [返回首页](./index.md)        [下篇Week15](./week15.md)
