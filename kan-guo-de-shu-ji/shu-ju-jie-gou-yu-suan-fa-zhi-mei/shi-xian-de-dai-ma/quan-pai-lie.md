```
#include<iostream>
#include<algorithm>
#include<queue>
#include<string>
using namespace std;
int a[] = {1,2,3,4};
priority_queue<int,vector<int>,greater<int> >s;
//priority_queue<int,vector<int>,less<int> >s;
void printPermutations(int data[],int n, int k)
{
	if(k==1)
	{
		int c=0;
		for(int i=0;i<n;i++)
			c=c*10+data[i];
		s.push(c);
	}
	
	for(int i=0;i<k;i++)
	{
		swap(data[i],data[k-1]);
		printPermutations(data,n,k-1);
		swap(data[i],data[k-1]);
	}
}

int main()
{
	printPermutations(a,4,4);
	while(!s.empty())
	{
		cout<<s.top()<<endl;
		s.pop();
	}
	return 0;
}
```



