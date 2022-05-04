## 01背包
- 题意：n个物品，每一个物品只能选一次，体积不超过m能得到的最大价值。

- 状态方程：
```c++
f[i][j]=f[i-1][j];//放不下的情况 
if(j>=v[i]) f[i][j]=max(f[i][j],f[i-1][j-v[i]]+w[i]);//第i个物品选不选 
```
- 代码：

```c++
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
const int N=1010;
int f[N][N];
int v[N],w[N];
int n,m;
int main(){
	cin>>n>>m;
	for(int i=1;i<=n;i++) cin>>v[i]>>w[i];
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			f[i][j]=f[i-1][j];//放不下的情况 
			if(j>=v[i]) f[i][j]=max(f[i][j],f[i-1][j-v[i]]+w[i]);//第i个物品选不选 
		}
	}
	cout<<f[n][m]<<endl;
}
```

一维01背包代码
```c++
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'

const int N=1010;

int f[N];
int v[N],w[N];
int n,m;
int main(){
	cin>>n>>m;
	for(int i=1;i<=n;i++) cin>>v[i]>>w[i];
	for(int i=1;i<=n;i++){
		for(int j=m;j>=v[i];j--){
		    f[j]=max(f[j-v[i]]+w[i],f[j]);
		}
	}
	cout<<f[m]<<endl;
}
```

## 完全背包
- 题意：n种物品，每种物品无限多个，求体积不超过m的最大价值。
- 动态转移方程：

```c++
f[i , j ] = max( f[i-1,j] , f[i-1,j-v]+w ,  f[i-1,j-2*v]+2*w , f[i-1,j-3*v]+3*w , .....)
f[i , j-v]= max(            f[i-1,j-v]   ,  f[i-1,j-2*v] + w , f[i-1,j-2*v]+2*w , .....)
由上两式，可得出如下递推关系： 
                        f[i][j]=max(f[i,j-v]+w , f[i-1][j]) 
```

- 代码：

```c++
#include<bits/stdc++.h>
using namespace std;
int n,m,k,V;
int a[N];
int v[N],w[N];//v代表体积，w代表质量
int f[N][N]; //在前i个中选，体积不超过j的最大值
int main(){
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		cin>>v[i]>>w[i];
	}
	for(int i = 1 ; i <=n ;i++)
	for(int j = 0 ; j <=m ;j++)
	{
    	f[i][j] = f[i-1][j];
    	if(j-v[i]>=0)
        f[i][j]=max(f[i][j],f[i][j-v[i]]+w[i]);
	}
	cout<<f[n][m]<<endl;
	return 0;
}
```

## 多重背包

最朴素的做法，枚举选多少个第i个物品，个数有限。
```c++
#include<bits/stdc++.h>
using namespace std;
const int N = 110;
int n, m;
int v[N], w[N], s[N];
int f[N][N];
int main()
{
    cin >> n >> m;

    for (int i = 1; i <= n; i ++ ) cin >> v[i] >> w[i] >> s[i];

    for (int i = 1; i <= n; i ++ )
        for (int j = 0; j <= m; j ++ )
            for (int k = 0; k <= s[i] && k * v[i] <= j; k ++ )
                f[i][j] = max(f[i][j], f[i - 1][j - v[i] * k] + w[i] * k);

    cout << f[n][m] << endl;
    return 0;
}
```
多重背包有一个二进制的优化，
[很菜，目前看不懂](https://www.acwing.com/solution/content/5527/) 

## 分组背包

每一组中只能选择一个，问体积不超过m的最大值。


```c++

#include<bits/stdc++.h>
using namespace std;

const int N=110;
int f[N][N];  //只从前i组物品中选，当前体积小于等于j的最大值
int v[N][N],w[N][N],s[N];   //v为体积，w为价值，s代表第i组物品的个数
int n,m,k;

int main(){
    cin>>n>>m;
    for(int i=1;i<=n;i++){
        cin>>s[i];
        for(int j=0;j<s[i];j++){
            cin>>v[i][j]>>w[i][j];  //读入
        }
    }

    for(int i=1;i<=n;i++){
        for(int j=0;j<=m;j++){
            f[i][j]=f[i-1][j];  //不选
            for(int k=0;k<s[i];k++){
                if(j>=v[i][k])     f[i][j]=max(f[i][j],f[i-1][j-v[i][k]]+w[i][k]);  
            }
        }
    }
    cout<<f[n][m]<<endl;
}

```


## 线性dp

转态转移方程通常是线性的。

#### 数字三角形

- 状态方程：

```c++
//每一个状态都可以由他左上角和上方转移
f[i][j]=a[i][j]+max(f[i-1][j-1],f[i-1][j]);
```

代码：

```c#
//这个题目也可以采用逆序的处理，不用处理边界
#include<bits/stdc++.h>
using namespace std;
int a[1010][1010];
int f[1010][1010];
int n;
int main(){
    cin>>n;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=i;j++){
            cin>>a[i][j];
        }
    }
    for(int i=1;i<=n;i++){
        for(int j=0;j<=i+1;j++){//初始化，注意边界初始化，因为当遍历到最右边的点时可能判断得到。
            f[i][j]=-1e9;
        }
    }
    f[1][1]=a[1][1];
    for(int i=2;i<=n;i++){
        for(int j=1;j<=i;j++){
            f[i][j]=a[i][j]+max(f[i-1][j-1],f[i-1][j]);
        }
    }
    int ans=-1e9;
    for(int i=1;i<=n;i++) ans=max(ans,f[n][i]);//问的是到最后一行的和最大值是多少。
    cout<<ans<<endl;
}
```

#### 最长上升子序列

- 题意：给一个长度为N的数列，问严格单调递增的子序列的长度最长是多少。
- 转移方程：

```c++
f[i] = max(f[i], f[j] + 1);
```

- 代码：

```c
#include <iostream>
using namespace std;
const int N = 1010;
int n;
int w[N], f[N];
int main() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> w[i];
    int mx = 1;    // 找出所计算的f[i]之中的最大值，边算边找
    for (int i = 0; i < n; i++) {
        f[i] = 1;    // 设f[i]默认为1，找不到前面数字小于自己的时候就为1
        for (int j = 0; j < i; j++) {
            if (w[i] > w[j]) f[i] = max(f[i], f[j] + 1);    // 前一个小于自己的数结尾的最大上升子序列加上自己，即+1，如果是非递减可以改成>=
        }
        mx = max(mx, f[i]);
    }
    cout << mx << endl;
    return 0;
}
```

#### 最长上升子序列II

- 相比上一题，题意是一样的的，但是数据范围更强了，DP的做法$O(n^2)$,会超时。
- 数据范围$0<=n<=100000$

- 思路：这一题贪心+二分 $O(nlogn)$

我们可以用一个数组$f[]$​,记录当前长度的上升序列的最后一位的最小值，维护这个数组使他最长，这部分就是贪心的策略，只有让前一位的最小，后面才能接上更多的数，让上升序列的长度更大，最后这个数组的长度就是答案。
我们可以分成两种情况：

1. 如果接下来的数$a[i]>f[cnt]$,那么他就可以直接接到数组的最后，长度+1；
2. 如果接下来的数$a[i]<f[cnt]$,那么就找到$f[cnt]$中第一个大于$a[i]$的数$f[tmp]$,并将$f[tmp]$更新为$a[i]$;

代码：

```c++
#include<bits/stdc++.h>
using namespace std;
const int  N=1000010;
int a[N],f[N];
int n,cnt=0;

int find(int x){//f[cnt]是一个单调递增的数组所以可以采用二分查找。
	int l=1,r=cnt;
	while(l<r){
		int mid=(l+r)>>1;
		if(f[mid]>=x) r=mid;
		else l=mid+1;
	}
	return  l;
} 
int main(){
    ios::sync_with_stdio(false);
    cin>>n;
    for(int i=1;i<=n;i++) cin>>a[i];
    f[++cnt]=a[1];
    for(int i=2;i<=n;i++){
        if(a[i]>f[cnt]) f[++cnt]=a[i];//大于最后一个最小的值，那么就直接加在最后面。
        else {
            int temp=find(a[i]);//更新前面的值，保存最小的那个值
            f[temp]=a[i];
        }
    }
    cout<<cnt<<endl;
    return 0;
}
```
#### 最长公共子序列

- 题意：给定两个长度分别为 N 和 M 的字符串 A 和 B，求既是 A 的子序列又是 B 的子序列的字符串长度最长是多少。
- 动态转移方程：

![ ](https://uploadfiles.nowcoder.com/images/20210601/890643981_1622544182143/F5551C2DBAFDF61E0E951B28C81C6F54 "图片标题") 
```c++
if(a[i]==b[j])   f[i][j]=f[i-1][j-1]+1;
else             f[i][j]=max(f[i-1][j],f[i][j-1]);
     
```

- 代码     ：
时间、空间复杂度：$O(n^2)$

```java
#include<bits/stdc++.h>
using namespace std;

const int N=10010;
char a[N],b[N];
int f[N][N];

int main(){
    int n,m;
    cin>>n>>m>>a+1>>b+1;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
           if(a[i]==b[j]) f[i][j]=f[i-1][j-1]+1;
           else {
               f[i][j]=max(f[i-1][j],f[i][j-1]);
           }
        }
    }
    cout<<f[n][m]<<endl;
    return 0;    
}
```

#### [最短编辑距离](https://www.acwing.com/problem/content/904/) 

![图片说明](https://uploadfiles.nowcoder.com/images/20210723/890643981_1627042497447/3FF3BB8071D3A897B14F0485C53A497B "图片标题") 


**思路**

**状态表示**
> $dp[i][j]$
>
> 表示1~ a[i],编辑成1~ b[j]的最小操作步数

**状态转移方程**

> 三种操作：
> 1.删除操作
> $dp[i][j]=dp[i-1][j]+1;$​​
> 2.插入操作
> $dp[i][j]=dp[i][j-1]+1;$​
> 3.替换操作
> $dp[i][j]=dp[i-1][j-1]+1;$

**代码**
```c++
#include<bits/stdc++.h>
using namespace std;
#define bug(x) cerr<<#x<<" : "<<x<<endl;
const int N=1e3+20;
const int mod=1e9+7;
const int INF=2e9;
typedef long long ll;


char a[N],b[N];
int n,m,dp[N][N];



int main(){
	//int T;cin>>T;while(T--){}
	scanf("%d",&n);
	scanf("%s",a+1);
	scanf("%d",&m);
	scanf("%s",b+1);
	
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			dp[i][j]=INF;//因为要去最小值，应该赋初值为极大值，不然会出问题
		}
	}
	for(int i=1;i<=n;i++) dp[i][0]=i;//处理边界，
	for(int i=1;i<=m;i++) dp[0][i]=i;
	
	
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			dp[i][j]=min(dp[i-1][j]+1,dp[i][j-1]+1);//插入、删除
			if(a[i]==b[j]) dp[i][j]=min(dp[i-1][j-1],dp[i][j]);
			else dp[i][j]=min(dp[i][j],dp[i-1][j-1]+1);//替换
		}
	}
	cout<<dp[n][m]<<endl;
	
}

/*
状态表示
dp[i][j]
表示1~a[i],编辑成1~b[j]的最小操作步数

状态转移方程
三种操作：
1.删除操作
dp[i][j]=dp[i-1][j]+1;
2.插入操作
dp[i][j]=dp[i][j-1]+1;
3.替换操作
dp[i][j]=dp[i-1][j-1]+1;
 */
```

## 区间DP

#### 石子合并

**题意：**合并 N 堆石子，每次只能合并相邻的两堆石子，求最小代价。

**思路**：
合并一定是左边连续的一部分，和右边连续的一部分进行合并。

状态表示：
$f[i][j]$表示合并$i-j$堆的石子所需要花费的最小体力。
属性：Min
状态转移方程：
当$i<j$时，$f[i][j]=min(f[i][j],f[i][k]+f[k][j]+s[j]-s[i-1];$
当$i=j$时，$f[i][j]=0;$
时间复杂度：$O(n^{3})$

**代码：**

```c++
#include <bits/stdc++.h>
using namespace std;
#define bug(x) cerr<<#x<<" : "<<x<<endl;
#define x first
#define y second
const int N=2e3+10; 
typedef long long ll;

int a[N],s[N];

int f[N][N];

int main(){
	int n;
	cin>>n;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		s[i]=s[i-1]+a[i];//求前缀和，求合并i~j堆石子的消耗体力 
	}
	for(int len=1;len<=n;len++){
		for(int i=1;i+len<=n;i++){
			int j=i+len;
			f[i][j]=1e9;
			for(int k=i;k<=j-1;k++){
				 f[i][j] = min(f[i][j], f[i][k] + f[k + 1][j] + s[j] - s[i - 1]);
			}
		}
	}
	cout<<f[1][N]<<endl;
	
}
```

**区间DP模板：**

```c++
for (int i = 1; i <= n; i++) {
    dp[i][i] = 初始值
}
for (int len = 2; len <= n; len++)           //区间长度
    for (int i = 1; i + len - 1 <= n; i++) { //枚举起点
        int j = i + len - 1;                 //区间终点
        for (int k = i; k < j; k++) {        //枚举分割点，构造状态转移方程
            dp[i][j] = max(dp[i][j], dp[i][k] + dp[k + 1][j] + w[i][j]);
        }
   }
```

## 数位DP

#### 计数问题

求a~b，1 ~ 9各出现了多少次。

```c++
#include <bits/stdc++.h>
using namespace std;
#define bug(x) cerr<<#x<<" : "<<x<<endl;
#define x first
#define y second
const int N=2e4+10; 
const int mod=1e9+7;
typedef long long ll;

int dgt(int n){
	int res=0;
	while(n){
		
		res++;
		n/=10;
	}
	return res;
}

int cnt(int n,int i){
	int res=0,d=dgt(n);
	for(int j=1;j<=d;j++){
		int p=pow(10,j-1),l=n/p/10,r=n%p,dj=n/p%10;
		if(i) res += l*p;
		if(!i && l) res += (l-1)*p;
		if( (dj > i) && (i || l)) res += p;
		if( (dj == i) && (i || l)) res += r+1; 
	}
	return res;
}

int main(){
	int a,b;
	while(cin>>a>>b,a){
		if(a>b) swap(a,b);
		for(int i=0;i<=9;i++){
			cout<<cnt(b,i)-cnt(a-1,i)<<" ";
		}
		cout<<'\n';
	}
	return 0;
}

```