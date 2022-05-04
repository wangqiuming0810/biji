## 总括


返回int类型在二进制下1的个数

```c
int cnt = __builtin_popcount(num); 
```


```c
vector, 变长数组，倍增的思想
    size()  返回元素个数
    empty()  返回是否为空
    clear()  清空
    front()/back()
    push_back()/pop_back()
    begin()/end()
    []
    支持比较运算，按字典序

pair<int, int>
    first, 第一个元素
    second, 第二个元素
    支持比较运算，以first为第一关键字，以second为第二关键字（字典序）

string，字符串
    size()/length()  返回字符串长度
    empty()
    clear()
    substr(起始下标，(子串长度))  返回子串
    c_str()  返回字符串所在字符数组的起始地址

queue, 队列
    size()
    empty()
    push()  向队尾插入一个元素
    front()  返回队头元素
    back()  返回队尾元素
    pop()  弹出队头元素

priority_queue, 优先队列，默认是大根堆
    size()
    empty()
    push()  插入一个元素
    top()  返回堆顶元素
    pop()  弹出堆顶元素
    定义成小根堆的方式：priority_queue<int, vector<int>, greater<int>> q;

stack, 栈
    size()
    empty()
    push()  向栈顶插入一个元素
    top()  返回栈顶元素
    pop()  弹出栈顶元素

deque, 双端队列
    size()
    empty()
    clear()
    front()/back()
    push_back()/pop_back()
    push_front()/pop_front()
    begin()/end()
    []

set, map, multiset, multimap, 基于平衡二叉树（红黑树），动态维护有序序列
    size()
    empty()
    clear()
    begin()/end()
    ++, -- 返回前驱和后继，时间复杂度 O(logn)

    set/multiset
        insert()  插入一个数
        find()  查找一个数
        count()  返回某一个数的个数
        erase()
            (1) 输入是一个数x，删除所有x   O(k + logn)
            (2) 输入一个迭代器，删除这个迭代器
        lower_bound()/upper_bound()
            lower_bound(x)  返回大于等于x的最小的数的迭代器
            upper_bound(x)  返回大于x的最小的数的迭代器
    map/multimap
        insert()  插入的数是一个pair
        erase()  输入的参数是pair或者迭代器
        find()
        []  注意multimap不支持此操作。 时间复杂度是 O(logn)
        lower_bound()/upper_bound()

unordered_set, unordered_map, unordered_multiset, unordered_multimap, 哈希表
    和上面类似，增删改查的时间复杂度是 O(1)
    不支持 lower_bound()/upper_bound()， 迭代器的++，--

bitset, 圧位
    bitset<10000> s;
    ~, &, |, ^
    >>, <<
    ==, !=
    []

    count()  返回有多少个1

    any()  判断是否至少有一个1
    none()  判断是否全为0

    set()  把所有位置成1
    set(k, v)  将第k位变成v
    reset()  把所有位变成0
    flip()  等价于~
    flip(k) 把第k位取反
```



## 双端队列

```
定义：deque<int>q;
从前面插入一个数，q.push_front();
从前面删除一个数，q.pop_front();
从后面插入一个数，q.push_back();
从后面删除一个数，q.pop_back();
翻转：reverse(q.begin(),q.end());
排序：sort(q.begin(),q.end());
判断非空：q.empty();
长度：q.size();
清除：q.clear();
```
[**模板题**](https://ac.nowcoder.com/acm/problem/14661) 

实现一个数据结构，实现一下七种操作；
```c
1 a从前面插入元素a

2 从前面删除一个元素

3 a从后面插入一个元素

4 从后面删除一个元素

5 将整个容器头尾翻转

6 输出个数和所有元素

7 对所有元素进行从小到大排序
```

其实用vector模拟也可以，我一开始就是这么想的，发现还要双端队列这个东西。
```c
 定义vector<int>a;
1 a.insert(a.begin(),x);
2 a.erase(a.begin());
3 a.push_back(x);
4 a.erase(a.end()-1);
5 reverse(a.begin(),a.end());
6 a.size(); for(auto t:a) cout<<a[i]<<" ";
7 sort(a.begin(),a.end());
```

双端队列代码：
```c
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e6+10;
#define debug(x) cout << #x << ": " << x << endl;
#define MAXN 100005

ll qpow(ll a,ll b){
	ll res=1;
	while(b){
		if(b&1) res=res*a;
		b>>=1;
		a*=a;
	}
	return res;
}
deque<int>q;
int main(){;
	int n,m,x;
	cin>>n>>m;
	while(m--){
		int p,x;
		int op;
		scanf("%d",&op);
		if(op==1){
			scanf("%d",&x);
			q.push_front(x);
		}
		else if(op==2){
			//scanf("%d",&x);
			q.pop_front();
		}
		else if(op==3){
			scanf("%d",&x);
			q.push_back(x);
		}
		else if(op==4){
			//scanf("%d",&x);
			q.pop_back();
		}
		else if(op==5){
			reverse(q.begin(),q.end());
		}
		else if(op==6){
				cout<<q.size()<<endl;
				for(int i=0;i<q.size();i++){
					cout<<q[i]<<" ";
				}
				cout<<'\n'; 
		}
		else sort(q.begin(),q.end());
	}
}
```



## _int128_

> __int 128,不能使用普通的cin,cout,输入，输出，需要自己写一个输入输出的模板

```c
#include <bits/stdc++.h>

using namespace std;
 
void scan(__int128 &x)//输入
{
    x = 0;
    int f = 1;
    char ch;
    if((ch = getchar()) == '-') f = -f;
    else x = x*10 + ch-'0';
    while((ch = getchar()) >= '0' && ch <= '9')
        x = x*10 + ch-'0';
    x *= f;
}
void _print(__int128 x)//输出正数
{
    if(x > 9) _print(x/10);
    putchar(x%10 + '0');
}
void print(__int128 x)//输出输出负数
{
    if(x < 0)
    {
        x = -x;
        putchar('-');
    }
    _print(x);
}
int main()
{
    __int128 a, b;
    scan(a); scan(b);
    print(a + b);
    return 0;
}
```


[模板题](https://ac.nowcoder.com/acm/contest/18196/F) 

代码：
```c
#include <bits/stdc++.h>

using namespace std;
 
void scan(__int128 &x)//输入
{
    x = 0;
    int f = 1;
    char ch;
    if((ch = getchar()) == '-') f = -f;
    else x = x*10 + ch-'0';
    while((ch = getchar()) >= '0' && ch <= '9')
        x = x*10 + ch-'0';
    x *= f;
}
void _print(__int128 x)
{
    if(x > 9) _print(x/10);
    putchar(x%10 + '0');
}
void print(__int128 x)//输出
{
    if(x < 0)
    {
        x = -x;
        putchar('-');
    }
    _print(x);
}
int main()
{
    __int128 a, b,c;
    scan(a); scan(b);scan(c);
    print(a + b+c);
    return 0;
}
```



## bitset

可以用来处理二进制的数。

常用函数。

```c
#include<bits/stdc++.h>
using namespace std;

const int maxn = 10;

bitset<maxn>B;
int main(){
    cout<<B<<endl; // 所有位依次输出
    int pos =1;
    cout<<B.size()<<endl;             // 返回容器大小
    B.set(pos);   cout<<B<<endl;      // 将pos位置为1
    B.set();      cout<<B<<endl;      // 将所有位置都置为1 .
    cout<<B.count()<<endl  ;          // 容器中有几个1
    cout<<B[1]<<B[0]<<endl;           // 可以用下标直接访问 [0,n-1].
    cout<<B.any()<<endl;              // 所有位置中 是否有1的存在
    B.reset();     cout<<B<<endl;     // 所有位置都变为0
    B.reset(pos) ; cout<<B<<endl;     // 将pos位置为0
    B.flip();      cout<<B<<endl;     //翻转容器中的所有位
    B.flip(pos);    cout<<B<<endl;     //翻转pos位

    int x=9;
    bitset<3> bs(x);  cout<<bs<<endl;  // 可以直接将整数传入，自动变为2进制数，但是如果容器不够存会自动截断整数的前部
    string ss="1010111000000";
    bitset<10>c(ss); cout<<c<<endl;    //可以直接传入string 类型，但是如果容器不够，会自动截断string的后部分

    bitset<5>a(string("1010"));
    bitset<5>b(string("0011"));
    cout<<(a<<1)<<endl;       // 支持 移位 ，左移右移
    cout<<(a|b)<<endl;        //  支持 | ^ &  注意这里如果两容器的大小不一样是会报错

return 0;
}

```





