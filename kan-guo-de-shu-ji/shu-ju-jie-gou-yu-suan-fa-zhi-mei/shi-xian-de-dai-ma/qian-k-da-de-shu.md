```
#include<iostream>
#include<algorithm>
#define MAXN 10000
using namespace std;
int n,k;

void print(int *a,int n)
{
	for(int i=0;i<k;i++)
		cout<<a[i]<<" ";
	cout<<endl;
}

//快速排序
void Sort(int *a,int n,int l,int r,int k)
{
	if(l-r+1 == k) return;
	int i=l,j=r,key=a[l];
	while(i<j)
	{
		while(i<j && key<=a[j]) j--;
		swap(a[i],a[j]);
		while(i<j && a[i]<=key) i++;
		swap(a[i],a[j]);
	}
	
	if(r-i+1 == k) return;
	else if(r-i+1 > k) Sort(a,n,i+1,r,k);
	else Sort(a,n,l,i-1,k-(r-i+1));
}
 
int main()
{
	int *a = new int[MAXN];
	cin>>n>>k;
	for(int i=0;i<n;i++)
		cin>>a[i];
	Sort(a,n,0,n-1,k);
	print(a,k); 
} 
```



