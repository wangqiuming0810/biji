## **引入**：

**ST算法（Sparse Table）**，以求**最大值**为例，设$f[i,j]$​表示$[i,i+2^j-1]$​这个区间内的最大值，那么在询问到$[a,b]$​区间的最大值时答案就是$max(f[a,k], f[b-2^k+1,k])，$​其中$k$​是满足$2^k<=b-a+1$​(即长度)的最大的$k,$​即$k=[ln(b-a+1)/ln(2)]$​​。

具体关于$f[i][j]$​的推导，看这个文章，[Pecco](https://zhuanlan.zhihu.com/p/105439034) 

ST 表是用于解决 **可重复贡献问题** 的数据结构。不支持修改。



！！**ST表不能够动态更新，动态更新可以用树状数组或者线段树**



**可重复贡献问题** 是指对于运算$opt$ ，满足$xoptx=x$ ，则对应的区间询问就是一个可重复贡献问题。例如，最大值有$max(x,x)=x$ ，gcd 有 $gcd(x,x)=x$，所以 RMQ 和区间 GCD 就是一个可重复贡献问题。像区间和就不具有这个性质，如果求区间和的时候采用的预处理区间重叠了，则会导致重叠部分被计算两次，这是我们所不愿意看到的。另外， 还必须满足结合律才能使用 ST 表求解。

**动态规划预处理**
```c
for (int i = 1; i <= 21; ++i)
        for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        {
            Min[j][i] = min(Min[j][i - 1], Min[j + (1 << (i - 1))][i - 1]);
            Max[j][i] = max(Max[j][i - 1], Max[j + (1 << (i - 1))][i - 1]);
        }
```

$log$的预处理：
```c
for (int i = 2; i <= n; ++i)
        Log2[i] = Log2[i / 2] + 1;
```

**预处理函数**：


```c
void init(){
    for (int i = 2; i <= n; ++i)
        Log2[i] = Log2[i / 2] + 1;
    for (int i = 1; i <= 21; ++i)
        for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        {
            Min[j][i] = min(Min[j][i - 1], Min[j + (1 << (i - 1))][i - 1]);
            Max[j][i] = max(Max[j][i - 1], Max[j + (1 << (i - 1))][i - 1]);
        }
}
```

**区间查询最大值，最小值**

```c
int find(int l,int r){
	
        int s = Log2[r - l + 1];
        int ma = max(Max[l][s], Max[r - (1 << s) + 1][s]);
        //int mi = min(Min[l][s], Min[r - (1 << s) + 1][s]);
        return ma;
        //return mi;
}
```

完整：

```c
int n,m;
int Log2[N], Min[N][21], Max[N][21];
void init(){
    for (int i = 2; i <= n; ++i)
        Log2[i] = Log2[i / 2] + 1;
    for (int i = 1; i <= 21; ++i)
        for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        {
            Min[j][i] = min(Min[j][i - 1], Min[j + (1 << (i - 1))][i - 1]);
            Max[j][i] = max(Max[j][i - 1], Max[j + (1 << (i - 1))][i - 1]);
        }
}
int find(int l,int r){
	
        int s = Log2[r - l + 1];
        int ma = max(Max[l][s], Max[r - (1 << s) + 1][s]);//最大
        int mi = min(Min[l][s], Min[r - (1 << s) + 1][s]);//最小
        //return ma;
        return mi;
}
```
输入：
```c

for (int i = 1; i <= n; ++i)
    {
        int x = read();
        Min[i][0] = x;
        Max[i][0] = x;
    }
```

## [King of Range](https://ac.nowcoder.com/acm/contest/11256/K) 

给你一个序列$a_1~a_n$,m组查询，每一组查询问有多少对$(i,j)$,$a_{i}$到$a_{j}$最大值减最小值大于K。


RMQ+双指针

代码：

```c
#include <bits/stdc++.h>
#define MAXN 200000
#define bug(x) cerr<<#x<<" : "<<x<<endl;
typedef long long ll;
using namespace std;
int read()
{
    int ans = 0;
    char c = getchar();
    while (!isdigit(c))
        c = getchar();
    while (isdigit(c))
    {
        ans = ans * 10 + c - '0';
        c = getchar();
    }
    return ans;
}
int Log2[MAXN], Min[MAXN][21], Max[MAXN][21];
 
bool chk(int l,int r,int k){
     
        int s = Log2[r - l + 1];
        int ma = max(Max[l][s], Max[r - (1 << s) + 1][s]);
        int mi = min(Min[l][s], Min[r - (1 << s) + 1][s]);
        if(ma-mi>k) return true;
        return false;
}
 
int main()
{
    //freopen("in.txt", "r", stdin);
    //freopen("test.txt", "w", stdout);
    int n = read(), m = read();
    for (int i = 1; i <= n; ++i)
    {
        int x = read();
        Min[i][0] = x;
        Max[i][0] = x;
    }
    for (int i = 2; i <= n; ++i)
        Log2[i] = Log2[i / 2] + 1;
    for (int i = 1; i <= 21; ++i)
        for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        {
            Min[j][i] = min(Min[j][i - 1], Min[j + (1 << (i - 1))][i - 1]);
            Max[j][i] = max(Max[j][i - 1], Max[j + (1 << (i - 1))][i - 1]);
        }
    while(m--){
        int k=read();
        ll ans=0;
        for(int i=1,j=1;i<=n;i++){
            while(!chk(i,j,k)&&j<=n&&i<=j){
                j++;
            }
             
            if(j<=n) ans=ans+n-j+1;
        }
        cout<<ans<<endl;
    }
    return 0;
}
```



## [洛谷P2251](https://www.luogu.com.cn/problem/P2251)

给你一个长度为n序列，求从第m个数开始，每个数的前m个数最小的数是什么？

数据范围：$m<n,n<1000000$​



**ST表板子**,代码：

```c
#include<bits/stdc++.h>
using namespace std;
const int N=1e6+7;
int n,m;
int Log2[N], Min[N][21], Max[N][21];
void init(){
    for (int i = 2; i <= n; ++i)
        Log2[i] = Log2[i / 2] + 1;
    for (int i = 1; i <= 21; ++i)
        for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        {
            Min[j][i] = min(Min[j][i - 1], Min[j + (1 << (i - 1))][i - 1]);
            Max[j][i] = max(Max[j][i - 1], Max[j + (1 << (i - 1))][i - 1]);
        }
}
int find(int l,int r){
	
        int s = Log2[r - l + 1];
        int ma = max(Max[l][s], Max[r - (1 << s) + 1][s]);//最大
        int mi = min(Min[l][s], Min[r - (1 << s) + 1][s]);//最小
        //return ma;
        return mi;
}

int main(){
	scanf("%d%d",&n,&m);
	for (int i = 1; i <= n; ++i)
    {
        int x ;
        scanf("%d",&x);
        Min[i][0] = x;
        Max[i][0] = x;
    }
    init();
    for(int i=m;i<=n;i++){
    	cout<<find(i-m+1,i)<<endl;
    }
}
```

