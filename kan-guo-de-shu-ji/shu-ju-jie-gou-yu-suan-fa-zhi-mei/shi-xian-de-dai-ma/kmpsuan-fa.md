```
#include<iostream>
#include<cstring>
#define MAXN 1000
using namespace std;

void Next(char b[],int next[])
{
    int m = strlen(b);
    next[0] = 0;
    for(int i=1,j=0;i<m;i++)
    {
        while(j>0 && b[i] != b[j])
            j = next[j-1];
        if(b[i] == b[j])
            j++;
        next[i] = j;
    }

//int kmp(char a[],char b[],int next[])
//{
//	int n,m,i,j;
//	i=j=0;
//	n = strlen(a);
//	m = strlen(b);
//	Next(b,next);
//	while(i<n)
//	{
//		if(j>0 && b[j] != a[i])
//			j = next[j-1];
//		else if(b[j] == a[i])
//			j++;
//		i++;
//		if(j == m)
//			return i-j;
//	}
//		return -1;
//}

int kmp(char a[],char b[],int next[])
{
    int n,m;
    n = strlen(a);
    m = strlen(b);
    Next(b,next);
    for(int i=0,j=0;i<n;i++)
    {
        while(j>0 && b[j] != a[i])
            j = next[j-1];
        if(b[j] == a[i])
            j++;
        if(j == m)
            return i-m+1;
    }
    return -1;
}

int main()
{
    int next[MAXN] = {0};
    char a[MAXN],b[MAXN];
    cin>>a>>b;
    cout<<kmp(a,b,next)<<endl;
    return 0;
}
```

```

```



