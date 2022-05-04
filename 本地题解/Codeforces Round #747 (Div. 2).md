# [Codeforces Round #747 (Div. 2)](https://codeforces.com/contest/1594)

这一场下班，下早了，C思路在一个分类的地方错了，写了个假算法，一直WA然后两题就下班了，这一场难度相对以前的Div2难度小一点吧，主要还是我反应太慢了，每次把问题复杂化，每次div2就只能过两题，真的很菜。以后争取CF都写一个题解总结一下。



# A

给你一个n，要你求出两个数分别是  $l,r$,使得 $ l,l+1,l+2,l+3....,r-2,r-1,r$ 的和等于 n



一开始总在算前n项和，浪费好几分钟时间，最后发现根本解不出两个未知数的方程，后来仔细一想，我把前面的和都为0，最后一个数n，刚好全部和不就是n，然后ac了



代码：

```c++
#include<bits/stdc++.h>
using namespace std;
const int N=1000010;
typedef long long ll;
#define int long long
int n;
void solve(){
	cin>>n;
	cout<<-(n-1)<<" "<<n<<endl;
}
signed main(){
	int T;cin>>T;while(T--) solve();
}
```



# B

 这个题目其实没有看很久题目，我就已经知道做法了，就是二进制，可是我又看清题目，他就说直接求第k个，而我还在求前k个，搞了那么久，浪费好多时间，



code：

```c++
#include<bits/stdc++.h>
using namespace std;
const int N=1000010;
typedef long long ll;
#define int long long
int n;
const int mod=1e9+7;
ll qpow(ll a, ll b) {
    ll ans = 1;
    while (b) {
        if (b & 1) ans = ans * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return ans;
}
void solve(){
	int k;
	cin>>n>>k;
	if(n==2){
		cout<<k<<endl;
		return;
	}
	int pos=0;
	ll ans=0;
	while(k){
		if(k&1){
			ans=(ans%mod+qpow(n,pos))%mod;
		}
		pos++;
		k>>=1;
	}
	cout<<ans<<endl;
}
signed main(){
	int T;cin>>T;while(T--) solve();
}
```



# C

卡了最久的C

很容易可以看的出，答案最大就是2；所以判断0,1,2的三种情况；

- 0，当然就是字符全是c的时候

- 1,1的话我们就枚举每一个i，看看是否满足，如果满足直接输出，i要满足，那么i的倍数上的字符一定是c
- 2，直接输出n，n-1就是行了。



代码：

```c++
#include<bits/stdc++.h>
using namespace std;
const int N=1000010;
typedef long long ll;
int n;
char c;
void solve() {
    int n;
    char c;
    cin >> n >> c;
    string s;
    cin >> s;
    bool ok = true;
    for (char x : s) {
        ok &= x == c;
    }
    if (ok) {
        cout << 0 << "\n";
        return;
    }
    for (int i = 1; i <= n; ++i) {
        bool ok = true;
        for (int j = i; j <= n; j += i) {
            ok &= s[j - 1] == c;
        }
        if (ok) {
            cout << 1 << "\n";
            cout << i << "\n";
            return;
        }
    }
    cout << 2 << "\n";
    cout << n << " " << n - 1 << "\n";
}
int main(){
	
	int T;cin>>T;while(T--) solve();
}
```



# E1

很简单的一道排列组合,太晚了就睡觉去了，看都没看

第一个根节点有6选择，下面的节点每一个颜色都有两个颜色不能够选择，4种选择

总共节点个数是$2^{k}-1$ 个，那么  $ans=6*4^{2^{k}-2}$



代码：

```c++
#include<bits/stdc++.h>
using namespace std;
const int N=1000010;
typedef long long ll;
const int mod=1e9+7;
int n;
ll k;
ll qpow(ll a, ll b) {
    ll ans = 1;
    while (b) {
        if (b & 1) ans = ans * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return ans;
}
void solve(){
	cin>>k;
	cout<<6*qpow(4,(1ll<<k)-2)%mod<<endl;
}
int main(){
	//int T;cin>>T;while(T--) 
	solve();
}
```

