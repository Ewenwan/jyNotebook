```
#include<iostream>
#include<algorithm>
using namespace std;

int heap[1000];
int n;
int length = 0;

void maxHeapify(int a[],int i,int n)
{
	int r;
	while(2*i+1<n)
	{
		r = 2*i+1;
		if(r<n-1 && a[r+1] < a[r])
			r++;
		if(a[i] > a[r])
			swap(a[i],a[r]);
		i=r;
	}
}

void head_sort(int a[],int n)
{
	for(int i=n/2-1;i>=0;i--)
		maxHeapify(a,i,n);
	
	for(int i=n-1;i>0;i--)
	{
		swap(a[0],a[i]);
		maxHeapify(a,0,i);
	}
	
}

void _insert(int data,int *n)
{
	heap[(*n)++] = data;
	head_sort(heap,*n);
}



int main()
{
	int n;
	cin>>n;
	for(int i=0;i<n;i++)
		cin>>heap[i];
	
	head_sort(heap,n);
	
	_insert(1000,&n);
	
	for(int i=0;i<n;i++)
	{
		cout<<heap[i]<<" ";
	}
	return 0;
} 
```



