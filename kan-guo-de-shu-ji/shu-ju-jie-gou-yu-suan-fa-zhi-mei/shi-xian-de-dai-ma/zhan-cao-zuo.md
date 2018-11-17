```
#include<iostream>
#include<stack>
using namespace std;
struct node{
    int data;
};

stack<int>a;

void init()
{
    for(int i=0;i<10;i++)
        a.push(i);
}

void print(){
    stack<int>b;
    b=a;
    cout<<"-----------------"<<endl;
    while(!b.empty()){
        cout<<b.top()<<endl;
        b.pop();
    }
}

int main()
{
    init();
    print();
    a.pop();
    print();
    a.push(100);
    print();
    int x = a.top();
    print();
    printf("栈顶数据:%d",x);
    return 0;
}
```



