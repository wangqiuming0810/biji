# A

给你一个数组，去重，每个数只留下最后出现的那个数字。

$1<T<20,1<n<50,1<a_i<1000$

## 思路

签到题，从后往前输出第一个没有出现的数字就行了。用个桶记录每一个数是否出现。

**code**

```c
#include<bits/stdc++.h>
using namespace std;
#define int long long 
#define sc(n) scanf("%lld",&n)
#define SC(n,m) scanf("%lld%lld",&n,&m)
#define pr(n) printf("%lld\n",n);
#define fr(i,l,r) for(int i=l;i<=r;i++)
#define x first
#define y second
typedef pair<int,int> PII;
const int mod=1e9+7;
const int N=1000010;

int a[N];
signed main(){
	int T;
	cin>>T;
	while(T--){
		int n;
		sc(n);
		int cnt[10010]={0};
		fr(i,1,n){
			sc(a[i]);
		}
		vector<int> q;
		for(int i=n;i>=1;i--){
			if(!cnt[a[i]]){
				q.push_back(a[i]);
				cnt[a[i]]++;
			}
		}
		cout<<q.size()<<endl;
		for(int i=q.size()-1;i>=0;i--){
			cout<<q[i]<<" ";
		}
		cout<<endl;
	}
	
}

```



# B

给定一个长度为 n 的由小写字母构成的字符串 s。

请你构造一个长度为 k 的由小写字母构成的字符串 t。

要求，字符串 t 需满足：

1. 字符串 t 在字典序上大于字符串 s。
2. 字符串 t 的字母集是字符串 s 的字母集的子集。一个字符串的字母集是指该字符串包含的所有不同字母的集合，例如 `abadaba` 的字母集为 {a,b,d}。
3. 字符串 t 在字典序上尽可能小。

保证答案存在。



**输入样例**：

```
4
3 3
abc
3 2
abc
3 3
ayy
2 3
ba
```

**输出样例**

```
aca
ac
yaa
baa
```

## 思路

分成两种情况：

1. $k>n$​,长于原字符串后面的用最小的字符代替即可
2. $k<=n$​​,从后往前扫描看哪一个字符是否可以换成比他大的第一个字符。可以就把他更改为比他大的第一个字符，不行的话继续往前扫描，更改了字符的那个位置后面的都用最小的字符代替。

**code**:

```c
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;
const int N = 100010;
int t,n,m,k;
char s1[N],s2[N];
bool st[N];

char get_min(){
    for(int i=0;i<26;i++)
    if(st[i]) return i+'a';
    return -1;
}

char get_next(int t){
    for(int i=t+1;i<26;i++){
        if(st[i]) return i+'a';
    }
    return -1;
}

int main(){
    int T;
    scanf("%d",&T);
    while(T--){
        scanf("%d%d",&n,&k);
        scanf("%s",s1);
        memset(st,0,sizeof st);
        for(int i=0;i<n;i++){
            st[s1[i]-'a']=1;
        }
        if(k>n){
            printf("%s",s1);
            char c=get_min();
            for(int i=n;i<k;i++){
                printf("%c",c);
            }
            cout<<"\n";
        }
        else{
            s2[k]='\0';
           for(int i=k-1;i>=0;i--){
                char c=get_next(s1[i]-'a');
                if(c!=-1){
                    s2[i]=c;
                    for(int j=0;j<i;j++) s2[j]=s1[j];
                    break;
                }
                s2[i]=get_min();
           }
            puts(s2);
        }
    }
    return 0;
}
```



# C

给定一个长度为 n 的**环形数组** a0,a1,…,an−1。

现在要对该数组进行 m 次操作。

操作分为以下两种：

- 增值操作 `l r d`，将区间 [l,r][l,r] 上的每个元素都增加 dd。
- 求最小值操作 `l r`，输出区间 [l,r][l,r] 内的所有元素的最小值。

注意，数组是环形的，所以当 n=5n=5 时，区间 [3,1][3,1] 内的所有元素依次为 a3,a4,a0,a1。



## 思路

线段树维护最小值,

1. $l<=r$直接更新或查找这段区间，
2. $l>r$​,就分成$[l,n],[0,r]$​两端更新查找。

**code：**

```c
#include <iostream>
#include <cstring>
#include <algorithm>

using namespace std;

typedef long long LL;
const int N = 200010;
const LL INF = 1e18;

int n, m;
int w[N];

struct Node
{
    int l, r;
    LL dt, mn;
}tr[N * 4];

void pushup(int u)
{
    tr[u].mn = min(tr[u << 1].mn, tr[u << 1 | 1].mn);
}

void pushdown(int u)
{
    auto &root = tr[u], &l = tr[u << 1], &r = tr[u << 1 | 1];
    l.dt += root.dt, l.mn += root.dt;
    r.dt += root.dt, r.mn += root.dt;//懒标记下传
    root.dt = 0;
}

void build(int u, int l, int r)
{
    if (l == r) tr[u] = {l, r, 0, w[l]};
    else
    {
        tr[u] = {l, r};
        int mid = l + r >> 1;
        build(u << 1, l, mid), build(u << 1 | 1, mid + 1, r);
        pushup(u);
    }
}

void update(int u, int l, int r, int d)
{
    if (tr[u].l >= l && tr[u].r <= r)
    {
        tr[u].dt += d, tr[u].mn += d;
    }
    else
    {
        pushdown(u);
        int mid = tr[u].l + tr[u].r >> 1;
        if (l <= mid) update(u << 1, l, r, d);
        if (r > mid) update(u << 1 | 1, l, r, d);
        pushup(u);
    }
}

LL query(int u, int l, int r)
{
    if (tr[u].l >= l && tr[u].r <= r)
    {
        return tr[u].mn;
    }
    else
    {
        pushdown(u);
        int mid = tr[u].l + tr[u].r >> 1;
        LL res = INF;
        if (l <= mid ) res = query(u << 1, l, r);
        if (r > mid) res = min(res, query(u << 1 | 1, l, r));
        return res;
    }
}

int main()
{
    scanf("%d", &n);
    for (int i = 0; i < n; i ++ ) scanf("%d", &w[i]);
    build(1, 0, n - 1);
    scanf("%d", &m);
    while (m -- )
    {
        int l, r, d;
        char c;
        scanf("%d %d%c", &l, &r, &c);
        if (c == '\n')
        {
            if (l <= r) printf("%lld\n", query(1, l, r));
            else printf("%lld\n", min(query(1, l, n - 1), query(1, 0, r)));
        }
        else
        {
            scanf("%d", &d);
            if (l <= r) update(1, l, r, d);
            else update(1, l, n - 1, d), update(1, 0, r, d);
        }
    }

    return 0;
}
```

