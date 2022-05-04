# A

有 a 首 1分钟的歌，b 首 2 分钟的歌，c首 3 分钟的歌。要分在两场音乐会，问最小的差是多少。

傻逼题，一来就应该猜结论，不应该瞎搞瞎搞，想的太复杂。最后如果差值为 2 或者 3 ，都可以转化，或者说有更优的分法。

代码：

```c
#include<bits/stdc++.h>
using namespace std;
#define fi first
#define se second
#define endl '\n'
typedef long long ll;
const int N=5e5+10;
const int M=1e6+7;
ll n,m,k;
void solve(){
	ll a,b,c;
	cin>>a>>b>>c;
	cout<<(a+b*2+c*3)&1<<endl;
	
}
int main(){
	int T;
	cin>>T;
	while(T--){
		solve();
	}
}
```



# B

B很明显的一看就有思路的，要使和为sum-1;那肯定就是统计 数组中有多少个 1,0.

由题意，最多只能删除一个 1 ，若干个 0 ，所以答案就为 $cnt1 $* $2^{cnt0}$ ,注意long long

```c
#include<bits/stdc++.h>
using namespace std;
#define fi first
#define se second
#define endl '\n'
typedef long long ll;
const int N=5e5+10;
const int M=1e6+7;
ll n,m,k;

int a[N];
void solve(){
	cin>>n;
	ll x,c1=0,c2=0;
	for(int i=0;i<n;i++){
		cin>>x;
		if(x==1) c1++;
		if(x==0) c2++;
	}
	cout<<c1*(1ll<<c2)<<endl;
}

int main(){
	//cout<<1ll*(1ll<<59)<<endl;
	int T;
	cin>>T;
	while(T--){
		solve();
	}
}
```

# C

```c
#include<bits/stdc++.h>
using namespace std;
#define fi first
#define se second
#define endl '\n'
typedef long long ll;
const int N=5e5+10;
const int M=1e6+7;
ll n,m,k;
int check(string& s, char c)
{
    int l = 0, r = s.length()-1;
    int res = 0;
    while(l<r)
    {
        if(s[l] == s[r]) {l++,r--;continue;}
        if(s[l]!=s[r] && s[l] == c){l++; res++;continue;}
        if(s[l]!=s[r] && s[r] == c){r--; res++;continue;}
        return 1e6;
    }
    
    return res;
}
void solve()
{
    int ans = 1e6;
    int n;cin>>n;
    string s;cin>>s;
	for(char c = 'a'; c <= 'z'; c++)
	    ans = min(ans, check(s, c));
	cout<<(ans==1e6 ? -1 : ans) << '\n';
}
int main(){
	//cout<<1ll*(1ll<<59)<<endl;
	int T;
	cin>>T;
	while(T--){
		solve();
	}
}
```



# D

构造B数组使得，$\sum a[i]*b[i]$ 等于0

- 首先如果 n为偶数，很容易构造，每两个数之间，a[i], a[i+1] 可以构造出 $b[i] = -a[i+1],b[i+1] = a[i]$

- n 为奇数，那么我们就需要构造出三个数，$ a[i],a[i+1],a[i+2]$, 我们可以构造出 $$b[i]=a[i+1]+a[i+2,b[i+1]=-a[i],b[i+2]=-a[i]$$,前提得满足 $a[i+1]+a[i+2] !=0$,不满足就换一对数

```c
#include<bits/stdc++.h>
using namespace std;
#define fi first
#define se second
#define endl '\n'
typedef long long ll;
const int N=5e5+10;
const int M=1e6+7;
ll n,m,k;


int a[N];
void solve(){
	cin>>n;
	for(int i=0;i<n;i++) cin>>a[i];
	if(n%2==0){
		for(int i=0;i<n;i+=2) cout<<-a[i+1]<<" "<<a[i]<<" ";
		cout<<endl;
	}
	else{
		if(a[1]+a[2]!=0){
			cout<<(a[1]+a[2])<<" "<<-a[0]<<" "<<-a[0]<<" ";
		}
		else if(a[0]+a[2]!=0){
			cout<<-a[1]<<" "<<a[0]+a[2]<<" "<<-a[1]<<" ";
		}
		else if(a[0]+a[1]!=0){
			cout<<-a[2]<<" "<<-a[2]<<" "<<a[0]+a[1]<<" ";
		}
		for(int i=3;i<n;i+=2){
			cout<<-a[i+1]<<" "<<a[i]<<" ";
		}
		cout<<endl;
	}
}
int main(){
	int T;
	cin>>T;
	while(T--){
		solve();
	}
}
```

