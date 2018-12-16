```
#include<iostream>
#include<vector>
#include<queue>
#include<cstring>
#define MAXN 100
using namespace std;
vector<int>g[MAXN];
bool visited[MAXN];
int pre[MAXN];
queue<int>p;

void print(int pre[],int s,int t)
{
    if(pre[t]!=-1 && t!=s)
        print(pre,s,pre[t]);
    printf("%d ",t);
}

void BFS(int s,int t)
{
    p.push(s);
    visited[s] = true;
    while(!p.empty())
    {
        int v = p.front();
        p.pop();
        for(int i=0;i<g[v].size();i++)
        {
            int u = g[v].at(i);
            if(!visited[u])
            {
                pre[u] = v;
                if(u == t)
                {
                    print(pre,s,t);
                    return ;
                }
            }
            visited[u] = true;
            p.push(u);
        }
    }
}

int main()
{

    int n,m,a,b,s,t;
    cin>>n>>m>>s>>t;
    memset(visited,false,sizeof(visited));
    memset(pre,-1,sizeof(pre));
    for(int i=0;i<m;i++)
    {
        cin>>a>>b;
        g[a].push_back(b);
        g[b].push_back(a);
    }
    BFS(s,t);
    return 0;
} 

//7 9 0 6
//0 1
//0 3
//1 2
//1 4
//2 5
//3 4
//4 5
//4 6
//6 7
```



