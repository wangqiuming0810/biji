```c
#include <bits/stdc++.h>
using namespace std;
#define int long long 
#define endl '\n'
#define bug(x) cerr<<#x<<" : "<<x<<endl
#define ios ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
#define duipai freopen("in.txt", "r", stdin);freopen("test.txt", "w", stdout);
const int N=2e6+10; 
const int M=1e4+5;
const int mod=998244353;
typedef long long ll;
ll qkpow(ll a, ll b) {ll ans = 1%mod;while (b) {if (b & 1) ans = ans * a % mod;a = a * a % mod;b >>= 1;}return ans;}
ll getInv(ll a) { return qkpow(a, mod - 2); }  //求一个数的逆元




int n,m,x; 
void solve() {
  int n;
  cin >> n;
  vector<ll> cnt(n + 1);
  for (int i = 0; i < n; i++) {
    int x;
    cin >> x;
    cnt[x]++;
  }
  ll ans = 0;
  for (int i = 2; i < n; i++) {
    ans += cnt[i - 1] * cnt[i] * cnt[i + 1];
  }
  for (int i = 1; i < n; i++) {
    ans += cnt[i] * (cnt[i] - 1) / 2 * cnt[i + 1];
  }
  for (int i = 2; i <= n; i++) {
    ans += cnt[i - 1] * cnt[i] * (cnt[i] - 1) / 2;
  }
  for (int i = 2; i < n; i++) {
    ans += cnt[i - 1] * cnt[i + 1] * (cnt[i + 1] - 1) / 2;
  }
  for (int i = 2; i < n; i++) {
    ans += cnt[i + 1] * cnt[i - 1] * (cnt[i - 1] - 1) / 2;
  }
  for (int i = 1; i <= n; i++) {
    ans += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
  }
  cout << ans << "\n";
}


signed main(){
    int T;cin>>T;while(T--)
    solve();
}
```



```c
#include <bits/stdc++.h>
using namespace std;
 
vector<set<int>> ans(3);
 
void init(){
	ans[1].insert(1111111111);
	ans[2].insert(1000000000);
	for(int b = 1; b <= 9; b++){
		for(int c = 0; c < (1 << (b-1)); c++){
			int d = 0, e = 0;
			int p10 = 1;
			for(int j = 0; j < b; j++){
				if(c & (1 << j)){
					d += p10;
				} else {
					e += p10;
				}
				p10 *= 10;
			}
			for(int r = 0; r <= 9; r++){
				for(int s = 0; s <= 9; s++){
					ans[2].insert(d * r + e * s);
					if(r == s) ans[1].insert(d * r + e * s);
				}
			}
		}
	}
}
 
void solve(){
	int n, k;
	cin >> n >> k;
	cout << (*ans[k].lower_bound(n)) << '\n';
}
 
int main(){
	ios_base::sync_with_stdio(false), cin.tie(nullptr);
	init();
	int T;
	cin >> T;
	while(T--) solve();
}
```

