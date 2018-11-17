```
#include<iostream>
#include<algorithm>
#define MAXN 10000
using namespace std;
void print(int *a,int n)
{
	for(int i=0;i<n;i++)
		cout<<a[i]<<" ";
	cout<<endl;
}

void merge(int *a,int n,int l,int mid,int r)
{
	int *b = new int[n];
	int i=l,j=mid+1,k=0;
	
	while(i<=mid && j<=r){
		if(a[i]<=a[j])
			b[k++] = a[i++];
		else
			b[k++] = a[j++];
	}
	
	while(i<=mid)
		b[k++] = a[i++];
	while(j<=r)
		b[k++] = a[j++];
	
	for(int i=0;i<=r-l;i++)
		a[l+i] = b[i];

}


//归并排序 
void mergeSort(int a[],int n,int l,int r)
{
	if(l<r)
	{
		int mid = (l+r)/2;
		mergeSort(a,n,l,mid);
		mergeSort(a,n,mid+1,r);
		merge(a,n,l,mid,r);
	}
	if(l>=r)
	{
		cout<<"归并排序"; 
		print(a,n);
	}
	return ;
}

int partition(int *a,int l,int r)
{
	int v = a[r];
	int i = l;
	for(int j=l;j<=r-1;j++)
	{
		if(a[j] < v)
			swap(a[i++],a[j]);
	}
	swap(a[i],a[r]);
	return i;
}

//快速排序
void quickSort(int a[],int n,int l,int r)
{
	if(l<r){
		int q = partition(a,l,r);
		quickSort(a,n,l,q-1);
		quickSort(a,n,q+1,r);
	}
	cout<<"快速排序";
	print(a,n);
}
 
int main()
{
	int *a = new int[MAXN];
	int n;
	cin>>n;
	for(int i=0;i<n;i++)
		cin>>a[i];
	mergeSort(a,n,0,n-1);
	quickSort(a,n,0,n-1); 
} 
```



