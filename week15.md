# 程序设计思维与实践 第15周作业    [返回首页](./index.md)   [上篇 Week14](./week14.md)

## Porblem-魔咒词典
Time Limit: 8000/5000 MS (Java/Others)    Memory Limit: 32768/32768 K (Java/Others)
Total Submission(s): 20863    Accepted Submission(s): 4872


### Problem Description
哈利波特在魔法学校的必修课之一就是学习魔咒。据说魔法世界有100000种不同的魔咒，哈利很难全部记住，但是为了对抗强敌，他必须在危急时刻能够调用任何一个需要的魔咒，所以他需要你的帮助。

给你一部魔咒词典。当哈利听到一个魔咒时，你的程序必须告诉他那个魔咒的功能；当哈利需要某个功能但不知道该用什么魔咒时，你的程序要替他找到相应的魔咒。如果他要的魔咒不在词典中，就输出“what?”
 

### Input
首先列出词典中不超过100000条不同的魔咒词条，每条格式为：

[魔咒] 对应功能

其中“魔咒”和“对应功能”分别为长度不超过20和80的字符串，字符串中保证不包含字符“[”和“]”，且“]”和后面的字符串之间有且仅有一个空格。词典最后一行以“@END@”结束，这一行不属于词典中的词条。
词典之后的一行包含正整数N（<=1000），随后是N个测试用例。每个测试用例占一行，或者给出“[魔咒]”，或者给出“对应功能”。
 

### Output
每个测试用例的输出占一行，输出魔咒对应的功能，或者功能对应的魔咒。如果魔咒不在词典中，就输出“what?”
 

### Sample Input
```cpp
[expelliarmus] the disarming charm
[rictusempra] send a jet of silver light to hit the enemy
[tarantallegra] control the movement of one's legs
[serpensortia] shoot a snake out of the end of one's wand
[lumos] light the wand
[obliviate] the memory charm
[expecto patronum] send a Patronus to the dementors
[accio] the summoning charm
@END@
4
[lumos]
the summoning charm
[arha]
take me to the sky
```

### Sample Output
```cpp
light the wand
accio
what?
what?
```

### Idea

### Codes
```cpp
#include<iostream>
#include<string>
#include<cstdio>
#include<map> 
#define ULL unsigned long long 
const int maxn=2e5+5;
using namespace std;  
const ULL seed=7;
const ULL mod=1e9;
string str,a,b; int N,tot;
map<ULL,int> Dir;
string words[maxn];
ULL getHash(string s){
    ULL h=0;
    for(int i=0;i<s.size();++i){
        h=(h*seed+(ULL)s[i])%mod;
    }    return h;
}
void strtodir( ){ 
    ULL Hash1=0,Hash2=0;
    int len=str.find("]");
    a=str.substr(1, len-1);
    b=str.substr(len+2, str.size()-1);
    words[tot++]=a;Dir.insert({getHash(a),tot});
    words[tot++]=b;Dir.insert({getHash(b),tot-2});
}
void findStr(){
    int l=0,r=str.size();    ULL h=0;
    if(str[0]=='[') {
        l=1;--r;
    }
    for(int i=l;i<r;++i){
        h=(h*seed+(ULL)str[i])%mod;
    }    
    if(Dir.find(h)!=Dir.end())    cout<<words[Dir[h]]<<endl; 
    else    cout<<"what?"<<endl; 
}
int main(){ 
    tot=0;
    while(true){ 
        getline(cin,str);  if(str=="@END@") break; 
        strtodir();
    }
    cin>>N;    cin.ignore();
    for(int i=0;i<N;++i){
        getline(cin,str);
        findStr();
    }
    return 0;
}
```

# 结束!     [返回首页](./index.md)  
