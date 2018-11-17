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


LinkedList create()
{
	Node *head,*p1,*tail;
	head = (Node *)malloc(sizeof(Node));
	
	head->next = head;
	tail = head;
	
	while(scanf("%d",&v)!=EOF && v!=-1)
	{
	   	Node *p;         
	    p = (Node *)malloc(sizeof(Node));
	    p->data = v;
	    p->next = head; // 新节点始终指向头结点 
	    
		tail->next = p;
		tail = p; 
	}
	return tail;
}

void print(LinkedList tail)
{
	//尾节点始终指向头结点 
	Node *head = tail->next;
	for(Node *start=head->next;start!=head;start=start->next)
		printf("%-4d",start->data);
	cout<<endl;
}



int main()
{
	LinkedList list;
 
	list = create();
	
	print(list);

	return 0;
} 

```



