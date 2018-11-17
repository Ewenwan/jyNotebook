```
#include<iostream>
#include<algorithm>
#define MAXN 10001
using namespace std;

void print(int a[],int n)
{
	for(int i=0;i<n;i++)
		cout<<a[i]<<" ";
	cout<<endl;
}

//冒泡排序 
void bubbleSort(int a[],int n)
{
	cout<<"冒泡排序";
	for(int i=0;i<n;i++)
	{
		bool flag = false;
		for(int j=0;j<n-i-1;j++)
		{
			if(a[j] > a[j+1])
			{
				flag = true;
				swap(a[j],a[j+1]);
			}
		}
		if(!flag)
			break;
	}
	print(a,n);
}

//插入排序 
void insertSort(int a[],int n){
	cout<<"插入排序";
	for(int i=1;i<n;i++)
	{
		int v= a[i];
		int j=i-1;
		for(;j>=0;j--)
		{
			if(a[j] > v)
				a[j+1] = a[j];
			else
				break;
		}
		a[j+1] = v;
	}
	print(a,n);
}

//选择排序
void selectionSort(int a[],int n){
	cout<<"选择排序";
	for(int i=0;i<n;i++)
	{
		int mini = a[i];
		int index = i;
		for(int j=i+1;j<n;j++)
		{
			if(mini < a[i])
			{
				mini = a[i];
				index = j;
			}
		}
		swap(a[i],a[index]);
	}
	print(a,n);
}

int main()
{
	int *a = new int[MAXN]; 
	int n;
	cin>>n; 
	for(int i=0;i<n;i++)
		cin>>a[i];
	bubbleSort(a,n);
	insertSort(a,n);
	selectionSort(a,n);
	return 0;
}
```



