# [Codeforces Round #726 (Div. 2)](https://codeforces.com/contest/1537)



# A

按题目给的意思瞎搞，就可以了



**code**

```c
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
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
int a[N];

signed main(){
	int T;sc(T);while(T--){
		sc(n);
		int sum=0;
		fr(i,1,n){
			sc(a[i]);
			sum+=a[i];
		} 
		if(sum==n){
			puts("0");
			continue;
		}
		int ans=0,tot=n;
		while(1){
			++n;
			if(n-sum>=0){
				break;
			}
		}
		ans=n-tot;
		pr(ans);
	}
	return 0;
}
```



# B

输出最右下角的那个角落就行了.

```c
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
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
int a[N];

signed main(){
	int T;sc(T);while(T--){
		int m,x,y;
		SC(n,m);SC(x,y);
		printf("%lld %lld %lld %lld\n",1ll,1ll,n,m);
	}
	return 0;
}
```



# C

找到差值最小的两个,作为中间点隔断,先输出后半部分,在输出前半部分就可以了.

**code**

```c
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
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
int a[N];

signed main(){
	int T;sc(T);while(T--){
		 cin >> n;
        vector<int> h(n);

        for (int i = 0;i < n; i++){
            cin >> h[i];
        }
        sort(h.begin(), h.end());

        if(n == 2){
            cout << h[0] << " " << h[1] << "\n";
            continue;
        }

        int pos = -1, mn = INT_MAX;

        for (int i = 1;i < n; i++){
            if(mn > abs(h[i] - h[i - 1])){
                pos = i;
                mn = abs(h[i] - h[i - 1]);
            }
        }
        
        for (int i = pos;i < n; i++){
            cout << h[i] << " ";
        }
        for(int i = 0;i < pos; i++){
            cout << h[i] << " ";
        }

        cout << "\n";
	}
	return 0;
}
```



# D

 <img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210808184138636.png" alt="image-20210808184138636" style="zoom:80%;" />



**code**

```c
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
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
int a[N];

signed main(){
	int T;sc(T);while(T--){
		sc(n);
		if(n&1) puts("Bob");
		else{
			int cnt = 0;
			while(n%2==0){
				cnt++;
				n>>=1;
			}
			//bug(cnt);
			if(n > 1||cnt % 2==0) puts("Alice");
			else puts("Bob");
		}
	}
	return 0;
}
```

