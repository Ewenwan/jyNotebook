```
#include<iostream>
#define MAXN 100000
using namespace std;

int *arr;
int length;


void init(){
	arr = new int[MAXN];
	length = 0;
	for(int i=0;i<10;i++){
		arr[i] = i;
		++length;
	}
}

void print(){
	printf("---------------------------\n");
	for(int i=length-1;i>=0;i--)
		cout<<arr[i]<<endl;
}

void pop(){
	if(length == 0){
		printf("empty");
		return;
	}
	--length;
}

int top(){
	if(length == 0){
		printf("empty");
		return -1;
	}
	int x = arr[length-1];
	return x;
}

void push(int x){
	if(length == MAXN){
		printf("full"); 
		return ;
	}
	arr[length] = x;
	++length;
}

int main()
{
	init();
	print();
	pop();
	print();
	push(100);
	print();
	int x = top();
	print();
	printf("栈顶数据:%d",x);
	return 0;
} 

```



