```
#include<iostream>
#include<cstdlib>
using namespace std;

typedef struct Node{
    int data;
    struct Node *next;
    struct Node *pre; 
}Node,*LinkedList;

int value;

LinkedList create()
{
    Node *tail,*head,*p;
    head = (Node *)malloc(sizeof(Node));
    p = tail = NULL;

    head->pre = NULL;
    head->next = NULL;

    tail = head;

    while(scanf("%d",&value)!=EOF && value != -1)
    {
        p = (Node *)malloc(sizeof(Node));
        p->data = value;
        p->next = NULL;

        p->pre = tail;
        tail->next = p;
        tail = p;
    } 

    return head;

}

void print(LinkedList head)
{
    for(Node *start=head->next;start!=head;start=start->next)
        printf("%-4d",start->data);
}

/*
将p节点插入在s节点后
//为p节点添加前后关系，并将s节点与后一节点的关系删除 
p->next = s->next;
s->next = p;
p->pre = s;
s->next->pre = p;//p->next->pre=p;
*/ 

/*
将s节点后的p节点删除 
//将p节点前后关系删除 
p=s->next;
s->next = p->next;
p->next->pre = s; 
free(p);
*/


/*
 head->pre = tail;
 tail->next = head; 
*/
int main()
{
    LinkedList list;
    list = create();
    print(list);
    return 0;
}
```



