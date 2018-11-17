```
#include<iostream>
#include<cmath>
#define eps 0.0000001
using namespace std;

int binary_search(int value,int a[],int n)
{
	int low=0,high=n;
	while(low<=high)
	{
		int mid = (low+high)/2;
		if(a[mid] == value)
			return mid;
		else if(a[mid] < value)
			low = mid+1;
		else
			high = mid-1;
	}
	return -1;
}

int main()
{
	int *a = new int[100];
	for(int i=0;i<=10;i++)
		a[i] = i*3;
	
	int value;
	cin>>value;
	
	int index = binary_search(value,a,10);
	printf("%d",index);
	return 0;
} 
```



