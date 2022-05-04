# BF

**BF算法，即暴力匹配算法，时间复杂度O（nm）；**
没什么讲的，代码：

```c
for(int i=0,j=0;i<s.size();i++){
		if(s[i]==p[j]){
			++i;
			++j;
		}
		else {
			i=i-j+1;
			j=0;
		}
		if(j==p.size()){
			//匹配成功 
		} 
	} 
```
# KMP匹配

先上模板。

**模板**

```c
void pre_kmp(string ss){//子串，求next数组
	int m=ss.size();
    nex[0]=-1;
    int i=0,j=-1;
    while(i<m){
        while(j!=-1&&ss[i]!=ss[j]) j=nex[j];
        nex[++i]=++j;
    }
}
int kmp(string str,string ss){//匹配str模式串,ss子串，可算重叠部分
	int len=str.size(),m=ss.size();
    memset(vis,0,sizeof vis);
    int i,j,cnt=0;
    i=j=0;
    while(i<len){    
        while(j!=-1&&str[i]!=ss[j]) j=nex[j];
        ++i;++j;
        if(j>=m) cnt++,j=nex[j],vis[i-1]=1;//如果不计算重叠部分，j=nex[j],去掉。
    }
    return cnt;
}
```



在暴力算法中可以发现，字符串中有些信息是可以在利用的，在回溯的过程我们只需要回溯到s串后缀与p数组前缀相等的地方，之后再继续比较，可以降低之间复杂度
**比如下面这个情况**
![图片说明](https://uploadfiles.nowcoder.com/images/20210423/890643981_1619169353302/5516EEC26CD3394589883F481CD239B7 "图片标题") 

**可以直接移到后缀和前缀相等的地方，即j=next[j]**

![图片说明](https://uploadfiles.nowcoder.com/images/20210423/890643981_1619169432976/292A454F6B726783A7C31995873E9A9A "图片标题") 

**这些模板的next数组与真实next数组相差1**

### 从1下标开始写的代码

```c
// s[]是长文本，p[]是模式串，n是s的长度，m是p的长度
//求模式串的Next数组：
//字符串从1开始
for (int i = 2, j = 0; i <= m; i ++ )
{
    while (j && p[i] != p[j + 1]) j = ne[j];
    if (p[i] == p[j + 1]) j ++ ;
    ne[i] = j;
}
// 匹配
for (int i = 1, j = 0; i <= n; i ++ )
{
    while (j && s[i] != p[j + 1]) j = ne[j];
    if (s[i] == p[j + 1]) j ++ ;
    if (j == m)
    {
        j = ne[j];
        // 匹配成功后的逻辑
    }
}
```
### 从0下标开始的代码

```c
    ne[0]=-1;
	for(int i=1,j=-1;i<m;i++){
		while(j>=0&&p[i]!=p[j+1]) j=ne[j];
		if(p[j+1]==p[i]) j++;
		ne[i]=j;
	} 
	for(int i=0,j=-1;i<n;i++){
		while(j>=0&&s[i]!=p[j+1]) j=ne[j];
		if(s[i]==p[j+1]) j++;
		if(j==m-1){
			j=ne[j];//回溯最长相同前后缀的地方为下一次匹配做准备
               //匹配成功后按题意输出 
		}
	}
```
# 求next数组

求next数组其实跟kmp匹配一样，只不过是模式串自己匹配自己，需要让i，j；错开就可以匹配p字符串的前后缀，求出当前的最长长度，就是next的值。代码在上面
其实就是**自己匹配自己**，理解这个就能写代码了；
![图片说明](https://uploadfiles.nowcoder.com/images/20210423/890643981_1619169931072/BCCC4828521720401F6EF8D08950F374 "图片标题") 

# 模板题：

[KMP字符串匹配](https://www.luogu.com.cn/problem/P3375) 

代码：
```c++
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define sc(n) scanf("%d",&n);
#define ios ios::sync_with_stdio(false);cin.tie(0); cout.tie(0)
typedef long long ll;
const int MOD=1000000007;
const int N=100010;
int a[N];
string s,p;
int ne[N]; 
int main(){
	//BF匹配算法 
//	string s,p;
//	for(int i=0,j=0;i<s.size();i++){
//		if(s[i]==p[j]){
//			++i;
//			++j;
//		}
//		else {
//			i=i-j+1;
//			j=0;
//		}
//		if(j==p.size()-1){
//			//匹配成功 
//		} 
//	} 
	string s,p;
	cin>>s>>p;
	int n=s.size();
	int m=p.size();
	ne[0]=-1;
	for(int i=1,j=-1;i<m;i++){
		while(j>=0&&p[i]!=p[j+1]) j=ne[j];
		if(p[j+1]==p[i]) j++;
		ne[i]=j;
	} 
	for(int i=0,j=-1;i<n;i++){
		while(j>=0&&s[i]!=p[j+1]) j=ne[j];
		if(s[i]==p[j+1]) j++;
		if(j==m-1){
			cout<<i-j+1<<endl;
			j=ne[j];//回溯最长相同前后缀的地方为下一次匹配做准备 
		}
	}
	for(int i=0;i<m;i++) cout<<ne[i]+1<<" "; 
	return 0;
}
/*
*/

```
**注：每次匹配成功之后一次，j一定要回溯到next[j]的位置，**

# [子串](https://ac.nowcoder.com/acm/problem/13253)



给出一个正整数n，我们把1..n在k进制下的表示连起来记为s(n,k)，例如s(16,16)=123456789ABCDEF10, s(5,2)=11011100101。现在对于给定的n和字符串t，我们想知道是否存在一个k(2 ≤ k ≤ 16)，使得t是s(n,k)的子串。

**暴力+KMP**

遍历k从2~16；计算每一个k下是否满足。

**code**：

```c
#include<bits/stdc++.h>
using namespace std;
#define MAXN 1000005
int nex[MAXN];
int vis[MAXN];
void pre_kmp(string ss)//子串，求next数组
{
	int m=ss.size();
    nex[0]=-1;
    int i=0,j=-1;
    while(i<m)
    {
        while(j!=-1&&ss[i]!=ss[j]) j=nex[j];
        nex[++i]=++j;
    }
}
int kmp(string str,string ss)//匹配模式串
{
	int len=str.size(),m=ss.size();
    memset(vis,0,sizeof vis);
    int i,j,cnt=0;
    i=j=0;
    while(i<len)
    {
        while(j!=-1&&str[i]!=ss[j]) j=nex[j];
        ++i;++j;
        if(j>=m) cnt++,j=nex[j],vis[i-1]=1;
    }
    return cnt;
}

string change(int n,int k){
	string s="";
	while(n){
		if(n%k>=10) s+=n%k+'A'-10;
		else s+=n%k+'0';
		n/=k;
	}
	reverse(s.begin(),s.end());
	return s;
}

int main(){
	int n;
	string ss;
	cin>>n>>ss;
	for(int k=2;k<=16;k++){
		string str="";
		for(int i=1;i<=n;i++){
			str+=change(i,k);
		}
		pre_kmp(ss);
		if(kmp(str,ss)) {
			puts("yes");
			return 0;
		}
	}
	puts("no");
	return 0;
}

```

