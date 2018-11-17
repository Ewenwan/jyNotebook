```
#include<iostream>
#include<cstdlib>
using namespace std;

typedef struct Node{
    int data;
    struct Node *next;
}Node,*LinkedList;

int v;
int i;

//头插法
LinkedList createH()
{
    Node *head;
    head = (Node *)malloc(sizeof(Node)); //申请头结点空间
    head->next = NULL;

    while(scanf("%d",&v)!=EOF && v != -1) 
    {
           Node *p;         
        p = (Node *)malloc(sizeof(Node));
        p->data = v; 
        p->next = head->next;
        head->next = p;
    }
    return head;
}

//尾插法
LinkedList createT()
{
    Node *head,*p1;
    head = (Node *)malloc(sizeof(Node));
    head->next = NULL;
    p1 = head;
    while(scanf("%d",&v)!=EOF && v!=-1)
    {
           Node *p;         
        p = (Node *)malloc(sizeof(Node));
        p->data = v;
        p1->next = p;
        p1 = p; 
    }
    p1->next = NULL;
    return head;
}
void print(LinkedList list)
{
    for(Node *start=list->next;start!=NULL;start=start->next)
        printf("%-4d",start->data);
    cout<<endl;
}

//插入，在第i个位置插入value值 
LinkedList insert(int i,int value,LinkedList list)
{
    Node *pre;
    pre = list;
    for(int j=0;j<i;j++)
        pre = pre->next;
    Node *p = (Node *)malloc(sizeof(Node));
    p->data = value;
    p->next = pre->next;
    pre->next = p;
    return list;
}

LinkedList del(int i,LinkedList list)
{
    Node *pre = list;
    for(int j=0;j<i;j++)
        pre = pre->next;
    pre->next = pre->next->next;
    return list;

}

//删除指定值 
LinkedList del2(int value,LinkedList list)
{
    //去除头结点的指定值
    while(list->next->data != value && list->next)
        list = list->next;

    Node *p = list->next,*pre=list;    

    while(p != NULL)
    {
        if(p->data == value)
            pre->next = p->next;
        pre = p;
        p=p->next;
    }
    return list;

}

int main()
{
    LinkedList list1,list2,list;

//    list1 = createH();
    list2 = createT();

//    list = list1;
    list = list2;
    print(list);

    printf("输入插入的位置和值:");
    cin>>i>>v;

    insert(i,v,list);
    print(list);

    printf("输入删除的位置:");
    cin>>i;
    del(i,list); 
    print(list);


    printf("输入删除的值:");
    cin>>v;
    del2(v,list); 
    print(list);
    return 0;
}
```



