```
#include<iostream>
#include<cmath>
#define eps 0.0000001
using namespace std;

float binary_search2(float n)
{
    if (n < 0)
        return n; 
    float mid,last;
    float low, high;
    low=0, high = n>=1?n:1;
    mid = (low+high)/2;
    do {
        if(mid*mid > n)
            high=mid; 
        else 
            low=mid;
        last=mid;
        mid=(high+low)/2; 
    } while(abs(mid- last) >= eps);
    return mid; 
}

float binary_search(float n)
{
    if (n < 0)
        return n; 
    float low, high,mid;
    low=0,high=n,mid=(low+high)/2;
    while(fabs(mid*mid-n)>eps)
    {
		if(mid*mid < n)
			low = mid;
		else
			high = mid;
		mid=(high+low)/2;
	}
    return mid; 
}

int main()
{
    int v;
    cin>>v;
    double f = binary_search2(v);
    cout<<f<<endl;
    return 0;
}
```



