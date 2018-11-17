```cpp
#include<iostream>
#include<algorithm>
using namespace std;

//变体一：查找第一个值等于给定值的元素
int binary_search1(int a[],int n,int value)
{
	int low=0,high=n-1;
	while(low<=high)
	{
		int mid = (low)+((high-low)>>1);
		if(a[mid] == value)
		{
			if((mid == 0) || a[mid-1] != value)
				return mid;
			else
				high = mid-1;
		}
		else if(a[mid] < value)
			low = mid+1;
		else
			high = mid-1;
	}
	return -1;
}

//变体二：查找最后一个值等于给定值的元素
int binary_search2(int a[],int n,int value)
{
	int low=0,high=n-1;
	while(low<=high)
	{
		int mid = (high+low)/2;
		if(a[mid] == value)
		{
			if((mid == n-1) || a[mid+1] != value)
				return mid;
			else
				low = mid+1;
		}
		else if(a[mid] < value)
			low = mid+1;
		else
			high = mid-1;
	}
	return -1;
}

//变体三：查找第一个大于等于给定值的元素
int binary_search3(int a[],int n,int value)
{
	int low=0,high=n-1;
	while(low<=high)
	{
		int mid = (high+low)/2;
		if(a[mid] >= value)
		{
			if((mid == 0) || a[mid-1] < value)
				return mid;
			else
				high = mid-1;
		}
		else
			low = mid+1;
	}
	return -1;
}

//查找最后一个小于等于给定值的元素
int binary_search4(int a[],int n,int value)
{
	int low=0,high=n-1;
	while(low<=high)
	{
		int mid = (high+low)/2;
		if(a[mid] <= value)
		{
			if((mid == n-1) || a[mid+1] > value)
				return mid;
			else
				low = mid+1;
		}
		else
			high = mid-1;
	}
	return -1;
}

int main()
{
 int a[] = {1,3,4,5,6,8,8,8,11,18};
 int n = 10;
 int value;
 cin>>value;
 int bs1 = binary_search1(a,n,value);
 cout<<bs1<<endl;
 int bs2 = binary_search2(a,n,value);
 cout<<bs2<<endl;
 int bs3 = binary_search3(a,n,value);
 cout<<bs3<<endl;
 int bs4 = binary_search4(a,n,value);
 cout<<bs4<<endl;
}
```



