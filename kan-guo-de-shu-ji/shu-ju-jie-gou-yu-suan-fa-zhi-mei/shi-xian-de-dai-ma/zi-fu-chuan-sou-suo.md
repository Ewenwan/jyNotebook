```
#include<iostream>
#include<string>
#include<cmath>
#define MAXN 1000
using namespace std;

void bf(string a,string b)
{
    int asize = a.size();
    int bsize = b.size();
    int i,j;
    i=j=0;
    while(i<asize && j<bsize)
    {
        if(a[i] == b[j])
        {
            i++;
            j++;
        }
        else
        {
            i=i-j+1;
            j=0;
        }
    }
    if(j >= bsize)
         cout<< i-bsize <<endl;
    else
        cout<<-1<<endl;
}

long long Decimal(string s)
{
    long long  ans = 0;
    for(int j=0,i=s.size()-1;i>=0;i--,j++)
    {
        ans += (char(s[i])-'a')*pow(26,j);
    }
    return ans;
}

void rk(string s,string s1)
{
    int ans = Decimal(s1);
    int m = s1.size();
    string c;
    for(int i=0;i<s.size()-m+1;i++)
    {
        c = s.substr(i,m);
        if(Decimal(c) == ans)
            cout<<i<<endl;
    }
}

int main()
{
    string s,s1;
    cin>>s>>s1;
    bf(s,s1);
    rk(s,s1);
    return 0;
}
```

```
#include<iostream>
#include<algorithm>
#include<string>
#include<cstring>
#define MAXN 1000
using namespace std;

int bm(string a,string b)
{
    int array[MAXN];
    int suffix[MAXN];
    bool prefix[MAXN];
    int n = a.size();
    int m = b.size();

    memset(array,-1,sizeof(array));
    memset(suffix,-1,sizeof(suffix));
    memset(prefix,false,sizeof(prefix));

    for(int i=0;i<m-1;i++)
    {
        int j=i;
        int k=0;
        while(j>=0 && b[j] == b[m-1-k])
        {
            --j;
            ++k;
            suffix[k] = j+1;
        }
        if(j == -1)
            prefix[k] = true;
    }

    for(int i=0;i<m;i++)
        array[int(b[i])] = i;

    int i=0;
    while(i<=n-m)
    {
        int j;
        for(j=m-1;j>=0;j--)
            if(a[i+j] != b[j]) break;

        if(j<0)
            return i;

        int x = j-array[(int)a[i+j]];
        int y = 0;
        if(j < m-1)
        {
            y = m;
            int k = m-1-j;
            if(suffix[k] != -1)
                y = j-suffix[k]+1;
            else
                for(int r=j+2;r<=m-1;++r)
                    if(prefix[m-r] == true)
                    {
                        y = r;
                        break;
                    }
        }

        i=i+(j-array[(int)a[i+j]]);
    }
    return -1;
}

int main()
{
    string a,b;
    cin>>a>>b;
    cout<<bm(a,b);
    return 0;
}
```



