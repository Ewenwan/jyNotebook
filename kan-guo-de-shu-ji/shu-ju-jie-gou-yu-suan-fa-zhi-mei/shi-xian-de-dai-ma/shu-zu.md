```
#include<iostream>
#include<string>
using namespace std;

int n; 
int index;
int op;
int value;
int *array;
int length;

void del(int j)
{
    if(n > 0)
    { 
        if(n > j)
        {
            for(int i=j;i<n-1;i++)
            {
                array[i] = array[i+1];
            }
            n--;
        }
        else{
            printf("数组长度不够\n");
        }
    }
    else{
        printf("这是一个空数组\n");
    }
}

void add(int j,int v)
{
    //数组位置不够，扩充 
    if(n >= length)
    {
        int *new_array = new int[length*2];
        for(int i=0;i<n;i++)
            new_array[i] = array[i];
        array = new_array;
        length = 2*length;
    }
    //插入 
    for(int i=n;i>j;i--)
        array[i] = array[i-1];
    array[j] = v;
    ++n;
}

void init()
{
    printf("请输入指定大小的数组:");
    cin>>n;
    length = 2*n;
    printf("请创建数组:");
    array = new int[length];
    for(int i=0;i<n;i++)
        cin>>array[i];
}

void find(int v)
{
    if(n > 0)
    {
        for(int i=0;i<n;i++)
        {
            if(v == array[i])
            {
                cout<<"位置:"<<i<<endl;
            }
        }
    }
    else{
        printf("这是一个空数组\n");
    }
}


void print()
{
    for(int i=0;i<n;i++)
    {
        printf("%-4d",array[i]);
    }
    cout<<endl;
}

int main()
{
    init();

    printf("1.删除第j个位置的值\n");
    printf("2.插入值在第j个位置前\n");
    printf("3.查找指定的第一个值在第几个位置\n");
    printf("0.退出\n");

    while(true)
    {
        printf("请选择将要实行的操作:");
        cin>>op;
        switch(op){
            case 1:{
            printf("请输入将要删除的位置:");
            cin>>index;
            del(index);
            print();
            break;
        }
            case 2:{
            printf("请输入将要添加的位置以及值:");
            cin>>index>>value;
            add(index,value);
            print();
            break;
        }
            case 3:{
            printf("请输入将要查询的值:");
            cin>>value;
            find(value);
            print();
            break;
        }
            case 0:exit(0);
        }
    } 
    return 0;
}
```



