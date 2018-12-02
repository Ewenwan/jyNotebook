```
#include<iostream>
#include<algorithm>
#include<queue>
using namespace std;

priority_queue<int,vector<int>,less<int> >p1;
priority_queue<int,vector<int>,greater<int> >p2;

int main()
{
    int n,data;
    cin>>n;
    while(n--)
    {
        cin>>data;
        p1.push(data);
        p2.push(data);
    }

    while(!p1.empty())
    {
        cout<<p1.top();
        p1.pop();
    }
    cout<<endl;

    while(!p2.empty())
    {
        cout<<p2.top();
        p2.pop();
    }
    cout<<endl;
    return 0;
}
```



