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



