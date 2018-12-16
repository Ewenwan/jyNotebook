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
}

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
			cout<<i-m+1<<endl;
	}
}

int main()
{
	int next[MAXN] = {0};
	char a[MAXN],b[MAXN];
	cin>>a>>b;
	kmp(a,b,next);
	return 0;
}
```



