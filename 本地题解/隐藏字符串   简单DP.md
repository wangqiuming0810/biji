# 隐藏字符串  

给定一个由小写字母构成的字符串 $s$​。

我们称字符串 t 隐藏于字符串 s 中，如果它满足：

- 存在一个字符串 s 的子序列，与其一一对应。
- 该子序列的各个元素的**下标**可以构成一个等差序列。

例如，字符串 `aab` 就隐藏于字符串 `aaabb` 中，因为 `aaabb` 的第 1,3,51,3,5 个元素刚好可以构成 `aab`，而这恰好是一个公差为 22 的等差数列。

字符串 t 可能隐藏于字符串 s 中多次，这取决于共有多少个 s 的不同子序列满足与字符串 t 一一对应，且各个元素下标可以构成一个等差数列。

例如，在字符串 `aaabb` 中，`a` 隐藏了 33 次，`b` 隐藏了 22 次，`ab` 隐藏了 66 次…

现在，请你求出字符串 s 中，隐藏次数最多的字符串一共隐藏了多少次？

**输入格式**

一个字符串 s ;

**数据范围**

$1<=|s|<=10^5$

**输入样例**

```c
aaabb
abcde
lol
```

**输出样例1**

```
6
1
2
```



# 解题思路

理解理解样例以后，能感觉得到，只需要求长度为1，2的子串出现的最多次数就行了。也可以证明，他的位置要构成等差数列，等差数列由首项和公差确定，而有前两项就能确定等差数列，枚举每一个等差数列，其实枚举前两个就行了。那应该怎么计算呢?

两种情况

- 长度为1，只需要统计每一个字符出现的次数就可以。
- 长度为2，设一个数组$f[i][j]$表示以第 i 个字符为结尾，和字符 j 构成长度为2的子串，出现的次数。



**code**

```c
#include<bits/stdc++.h>
using namespace std;
#define js ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define sc(n) scanf("%lld",&n)
#define SC(n,m) scanf("%lld%lld",&n,&m)
#define pr(n) printf("%lld\n",n);
#define fr(i,l,r) for(int i=l;i<=r;i++)
#define bug(x) cout<<#x<<" : "<<x<<endl;
#define int long long 
const int N=1000010;
const int M=10010;
const int mod=1e9+7;
int n;
int s[N],f[26][26];
char str[N];

signed main(){
	scanf("%s",str);
	int ans=0;
	for(int i=0;str[i];i++){
		int t=str[i]-'a';
		for(int j=0;j<26;j++){
			f[j][t]+=s[j];
			ans=max(ans,f[j][t]);
		}
		s[t]++;
		ans=max(ans,s[t]);
	}
	pr(ans);
	return 0;
}
```

