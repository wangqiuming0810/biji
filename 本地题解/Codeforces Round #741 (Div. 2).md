# A

给你一个区间  $[l,r]$,请你找出两个数，a，b使得a mod  b最大。



签到题, r%(r/2+1) 的值一定最大。



代码：

```c
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100010;
#define endl '\n'
int a[N];

int main(){
	int T;
	cin>>T;
	while(T--){
		int x,y;
		cin>>x>>y;
		//if(x>y) swap(x,y);
		int t=(y)/2+1;
		if(t<x){
			cout<<y-x<<endl;
		}
		else{
			if(y%2==0) cout<<y/2-1<<endl;
			else cout<<y/2<<endl;
		}
		
	}
}
```



# B

给你一个n位的整数，问你最多能删除多少位，让他变成非质数，1也是非质数，输出删除后的位数，和数字。



**思路**:

包含，1，4，6，8，9这样的直接输出就行了，而如果只包含质数2，3，5，7；特判25，27，32，35，57，75，72；

如果2，3，5，7中有一个数的个数大于2，则输出类似于22，33，55，77；



代码：

```c
#include <bits/stdc++.h>
using namespace std;
#define js ios::sync_with_stdio(false);cin.tie(0); cout.tie(0)
#define sc(x) scanf("%d",x)
typedef long long ll; typedef unsigned long long ull; typedef long double ld;
inline ll gcd(ll x, ll y) { return y ? gcd(y, x % y) : x; }
ll qpow(ll a, ll b) { ll ans = 1;    while (b) { if (b & 1)    ans *= a;        b >>= 1;        a *= a; }    return ans; }    
ll qpow(ll a, ll b, ll mod) { ll ans = 1;  a%=mod; while (b) { if (b & 1)(ans *= a) %= mod; b >>= 1; (a *= a) %= mod; }return ans % mod; }
inline ll read() { ll s = 0, w = 1; char ch = getchar(); while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();    return s * w; }

const int mod=1e9+7;
const int N=1e5+7;

int k;
ll n;
string s;

void fun(){
	cin>>k>>s;
	for(int i=0;i<k;i++){
		if((s[i]=='1'||s[i]=='4'||s[i]=='6'||s[i]=='8'||s[i]=='9')){
			cout<<1<<endl;
			cout<<s[i]<<endl;
			return;
		}
	}
	for(int i=0;i<k-1;i++){
		for(int j=i+1;j<k;j++){
			if(s[i]==s[j]){
				cout<<2<<endl;
				cout<<s[i]<<s[i]<<endl;
				return;
			}
			if(s[i]=='2'&&s[j]=='5'||s[i]=='2'&&s[j]=='7'||s[i]=='3'&&s[j]=='2'||s[i]=='3'&&s[j]=='5'||s[i]=='5'&&s[j]=='2'||s[i]=='5'&&s[j]=='7'||s[i]=='7'&&s[j]=='2'||s[i]=='7'&&s[j]=='5'){
					cout<<2<<endl;
				cout<<s[i]<<s[j]<<endl;
				return;
			}
		}
	}
}

int main(){
	int t;
	cin>>t;
	while(t--){
		fun();
	}   
	return 0; 
}

```

~~补题~~

# C

题目意思大概应该是，给你一个二进制字符串，然后你要选两段区间，这两个区间不能相同，把选到的两端区间里的字符串转化成10进制整数，假设t,w然后，t=w*k,两个区间长度都必须大于n/2,向下取整。



**思路：**

下标从0开始，思考的太慢了，其实很容易懂，
1.例：111他的两倍是1110，所以后半段有0我们可以直接构造两倍的关系
2.那前半段有0，例：0111 和 111其实是相等的，这就很好办了。
3.全是1，乱输出



代码：

```c
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000;
#define endl '\n'
int a[N],n;
string s;
//下标从0开始，思考的太慢了，其实很容易懂，
//1.例：111他的两倍是1110，所以后半段有0我们可以直接构造两倍的关系
//2.那前半段有0，例：0111 和 111其实是相等的，这就很好办了。
//3.全是1，乱输出
void solve(){
	cin>>n;
	cin>>s;
	for(int i=0;i<n;i++){
		if(s[i]=='0'){
			if(i>=n/2){
				cout<<1<<" "<<i+1<<" "<<1<<" "<<i<<endl;
				return;
			}
			else{//10110011
				cout<<i+2<<" "<<n<<" "<<i+1<<" "<<n<<endl;
				return;
			}
		}
	}
	cout<<1<<" "<<n-1<<" "<<2<<" "<<n<<endl;
}
int main(){
	int T;
	cin>>T;
	
	while(T--){
		solve();
	}
}
```



# D1

给你一个字符串，‘+’ 表示正电荷 ‘-’ 表示负电荷，即 + 表示1， - 表示-1；当i为偶数是当前位取反，给你q个询问，每一个询问一个区间$[l,r]$问最少删除几个字符最后 电荷为0，



瞎猜的

代码：

```c
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=2000010;
#define endl '\n'
int a[N],n;
string s;
void solve(){
	int q;
	cin>>n>>q;
	cin>>s;
	s=" "+s;
	for(int i=1;i<=n;i++){
		int c=s[i]=='+' ?1:-1;
		if(i&1) c=-c;
		a[i]=a[i-1]+c;
	}
	while(q--){
		int l,r;
		cin>>l>>r;
		int len=r-l+1;
		if(a[r]-a[l-1]==0){
			cout<<0<<endl;
		}
		else{
			if(len&1) cout<<1<<endl;
			else cout<<2<<endl;
		}
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





