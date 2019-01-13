```
#include<iostream>
#include<algorithm>
using namespace std;

struct things{
	int weight;
	int price;
	double ave;
}t[100];

int cmp(struct things &a,struct things& b)
{
	if(a.ave < b.ave)
		return true;
	else
		return false;
}

int main()
{
	int n,total,ans=0;
	cin>>n>>total;
	for(int i=0;i<n;i++){
		cin>>t[i].weight>>t[i].price;
		t[i].ave = (double)t[i].weight / t[i].price;
	}
	sort(t,t+n,cmp);
	for(int i=0;i<n;i++)
	{
		if(total >= t[i].weight){
			total -= t[i].weight;
			ans += t[i].price;
		}else{
			ans += total*t[i].ave;
		}
	}
	cout<<ans<<endl;
}

//5 100
//100 100
//30 90
//60 120
//20 80
//50 75
```



