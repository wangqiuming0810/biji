## T229470 A. 小智的疑惑

调用string的substr方法，暴力即可。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 5e5 + 7;
const int mod = 1e9 + 7;
const int MOD = 998244353;
#define int unsigned long long
#define rep(i, l, r) for (int i = l; i <= r; ++i)
vector<pair<int, int> > g[N];

int xorr[N];

void dfs(int u, int f, int val) {
    xorr[u] = val;
    for (int i = 0; i < g[u].size(); i++) {
        int next = g[u][i].first, w = g[u][i].second;
        if (next == f)
            continue;
        dfs(next, u, w ^ val);
    }
}

void solve() {
    int n, m, u, v, w, k;
    cin >> n >> m;
    for (int i = 1; i < n; i++) {
        cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }
    dfs(n-1, 0, 0);
    while (m--) {
        cin >> u >> v >> k;
        if ((xorr[u] ^ xorr[v]) == k) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }
}

signed main() {
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    solve();
    return 0;
}
```



## T229471 B. 三元组

三重循环暴力

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 2e6 + 7;
const int mod = 1e9 + 7;
const int MOD = 998244353;
#define int long long
#define rep(i, l, r) for (int i = l; i <= r; ++i)
int a[N];
void solve(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    int ans=0;
    for(int i=0;i<n;i++){
        for(int j=i;j<n;j++){
            for(int k=j;k<n;k++){
                if(a[i]+a[j]==a[k]) ans++;
            }
        }
    }
    cout<<ans<<endl;
}
signed main(){
    int _;
    cin>>_;
    while(_--) solve();
    return 0;
}
```



## T229472 C. 排排队

只要另一个数组有那个数组的数，交换$n^2$次就一定可以，排成想要的样子，冒泡 。

~~但是这一题我理解错题意了，我改b数组了。题意是改a数组，wa3~~

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 2e6 + 7;
const int mod = 1e9 + 7;
const int MOD = 998244353;
#define int long long
#define rep(i, l, r) for (int i = l; i <= r; ++i)
int a[N], b[N], c[N], d[N];
void solve() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        c[i]=a[i];
    }
    for (int j = 0; j < n; j++) {
        cin >> b[j];
        d[j]=b[j];
    }
    sort(c,c+n);
    sort(d,d+n);
    for(int i=0;i<n;i++){
        if(c[i]!=d[i]){
            cout<<"NO"<<endl;
            return;
        }
    }
    vector<int> ans;
    vector<int> res;
    for (int i = 0; i < n; i++) {
        if (a[i] == b[i])
            continue;
        int pos = -1;
        for (int j = i + 1; j < n; j++) {
            if (a[j] == b[i]) {
                pos = j;
            }
        }
        for (int j = pos; j > i; j--) {
            ans.push_back(j+1);
            res.push_back(j);
            swap(a[j], a[j - 1]);
        }
    }
    cout << "YES" << endl;
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " " << res[i] << endl;
    }
    cout << "0 0\n";
}
signed main() {
    int _;
    cin >> _;
    while (_--)
        solve();
    return 0;
}
```



## R71214110背单词的小智

二分答案 m，check的话，就优先从前面的那几个开始，判断他要背几天，和k相比较。

leetcode原题，leetcode410https://leetcode-cn.com/problems/split-array-largest-sum/

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 2e6 + 7;
const int mod = 1e9 + 7;
const int MOD = 998244353;
#define int long long
#define rep(i, l, r) for (int i = l; i <= r; ++i)
int a[N];

bool check(vector<int> &nums, int x, int m) {
    long long sum = 0;
    int cnt = 1;
    for (int i = 0; i < nums.size(); i++) {
        if (sum + nums[i] > x) {
            cnt++;
            sum = nums[i];
        } else {
            sum += nums[i];
        }
    }
    return cnt <= m;
}

int work(vector<int> &nums, int m) {
    long long left = 0, right = 0;
    for (int i = 0; i < nums.size(); i++) {
        right += nums[i];
        if (left < nums[i]) {
            left = nums[i];
        }
    }
    while (left < right) {
        long long mid = (left + right) >> 1;
        if (check(nums, mid, m)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
void solve() {
    int n, k;
    cin >> n >> k;
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
        nums[i] *= nums[i];
    }

    cout<<work(nums,k)<<endl;

}
signed main() {
        solve();
    return 0;
}
```

## T229475 F1. 生活在树上（easy version）

根据异或的性质，a到b的异或异或上a到c的异或。这中间点可以随意取，所以我们取一个根节点。如果存在 xor[u] ^ xor[v]== k。

树的DFS。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 5e5 + 7;
const int mod = 1e9 + 7;
const int MOD = 998244353;
#define int unsigned long long
#define rep(i, l, r) for (int i = l; i <= r; ++i)
vector<pair<int, int> > g[N];

int xorr[N];

void dfs(int u, int f, int val) {
    xorr[u] = val;
    for (int i = 0; i < g[u].size(); i++) {
        int next = g[u][i].first, w = g[u][i].second;
        if (next == f)
            continue;
        dfs(next, u, w ^ val);
    }
}

void solve() {
    int n, m, u, v, w, k;
    cin >> n >> m;
    for (int i = 1; i < n; i++) {
        cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w});
    }
    dfs(n-1, 0, 0);
    while (m--) {
        cin >> u >> v >> k;
        if ((xorr[u] ^ xorr[v]) == k) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }
}
signed main() {
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    solve();
    return 0;
}
```

