```
#include<iostream>
#include<vector>
#define MAXN 1000
using namespace std;
vector<int>g[MAXN];
int main()
{
	int n,m;
	cin>>n>>m;
	for(int i=0;i<m;i++)
	{
		int a,b;
		cin>>a>>b;
		g[a].push_back(b);
	}
	
	for(int i=1;i<=n;i++)
	{
		if(g[i].size())
			cout<<i<<"->";
		else
			cout<<i;
		for(int j=0;j<g[i].size();j++)
		{
		    cout<<g[i].at(j);
			if(j!=g[i].size()-1)
				cout<<"->";
		}
		cout<<endl;
	}
	return 0;
} 
//1 2
//2 3
//2 4
//2 5
//4 2
//5 3
//5 4
```



