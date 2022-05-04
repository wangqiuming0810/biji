<img src="C:\Users\wang\AppData\Roaming\Typora\typora-user-images\image-20210924185528126.png" alt="image-20210924185528126" style="zoom: 200%;" />

代码：

````c++
#include<bits/stdc++.h>
using namespace std;
const int N=100010;
const int INF=0x3f3f3f3f;
int a[N],mn[N<<2],need[N<<2],he[N],res=1,h=0;

void update(int rt,int l,int r,int x,int val){
	if(l==r){
		mn[rt]=val;
		return;
	}
	int mid=l+r>>1;
	if(x<=mid) update(rt<<1,l,mid,x,val);
	if(x>mid) update(rt<<1|1,mid+1,r,x,val);
	mn[rt]=min(mn[rt<<1],mn[rt<<1|1]);
}


int query(int rt,int l,int r,int x,int y){
	if(x<=l&&r<=y) return mn[rt];
	int mid=l+r>>1,ans=INF;
	if(x<=mid) ans=min(query(rt<<1,l,mid,x,y),ans);
	if(y>mid) ans=min(query(rt<<1|1,mid+1,r,x,y),ans);
	return ans;
}

int main(){
	int n,k;
	cin>>k>>n;
	for(int i=0;i<n;i++){
		int x,y;
		cin>>x>>y;
		if(i<k){//前面k个，先初始化 
			update(1,0,k-1,i,x+y);
			he[i]++;
			continue;
		}
		if(mn[1]>x) continue;//如果当前所有都不能满足，直接跳过
		int d=i%k,l,r,ans;
		int tot=query(1,0,k-1,d,k-1);
		if(tot<=x){
			l=d,r=k-1;//i%k的后半段 
		} 
		else{//i%k的前半段 
			l=0,r=d-1; 
		}
		//二分查找区间长度，确定位置最靠近左边的合适的位置
		while(l<=r){
			int mid=l+r>>1;
			if(query(1,0,k-1,l,mid)<=x) ans=mid,r=mid-1;
			else l=mid+1;
		} 
		update(1,0,k-1,ans,x+y);
		he[ans]++;
		res=max(res,he[ans]);//记录处理最多事件的数量
		//printf("res = %d\n",res); 
	}
	for(int i=0;i<k;i++){
		//printf("%d ",he[i]);
		if(he[i]==res) need[++h]=i;
	}
	//puts("");
	for(int i=1;i<=h;i++){
		if(i!=1) printf(" ");
		printf("%d",need[i]);
	}
} 
````

