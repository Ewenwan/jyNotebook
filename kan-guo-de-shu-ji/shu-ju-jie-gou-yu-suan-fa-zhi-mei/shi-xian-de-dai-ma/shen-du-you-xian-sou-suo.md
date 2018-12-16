```
#include<iostream>
#include<vector>
#include<cstring>
#define MAXN 1000
using namespace std;
vector<int>g[MAXN];
int pre[MAXN];
int visited[MAXN];
int n,m,a,b,s,t;

void print(int pre[],int s,int t)
{
	if(pre[t]!=-1 && t!=s)
		print(pre,s,pre[t]);
	printf("%d ",t);
}

void DFS(int u,int t)
{	
	visited[u] = true;
	if(u == t)
	{
		print(pre,s,t);
	//	return ;
		cout<<endl; 
	}
	for(int i=0;i<g[u].size();i++)
	{
		int v = g[u].at(i);
		if(!visited[v])
		{
			pre[v] = u;
//			cout<<v<<":"<<u<<endl;
			DFS(v,t);
		}
	}
	visited[u] = false;
}

int main()
{
	cin>>n>>m>>s>>t;
	memset(visited,false,sizeof(visited));
	memset(pre,-1,sizeof(pre));
	for(int i=0;i<m;i++)
	{
		cin>>a>>b;
		g[a].push_back(b);
		g[b].push_back(a);
	}
	DFS(s,t);
	return 0;
} 
//8 9 1 6
//1 2
//1 4
//2 3
//2 5
//3 6
//4 5
//5 6
//5 7
//7 8
```



