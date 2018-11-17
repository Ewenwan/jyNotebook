```
#include<iostream>
#include<stdlib.h>
using namespace std;

typedef struct node{
	int data;
	struct node *next;
}*List;

node *head,*tail;

//建立 
List create()
{
	tail = head = (node *)malloc(sizeof(node));
	head->next = NULL;
	tail->next = head;
	int x;
	while(scanf("%d",&x)!=EOF && x != -1){
		
		node *p2 = (node *)malloc(sizeof(node));
		p2->data = x;
		p2->next = NULL;
		tail->next = p2;
		tail = p2;
	}
	tail->next = head;
	
}


void print(List head){
	printf("--------------------我是分割线----------------------------\n");
	for(node* start=head->next;start!=head;start=start->next)
		cout<<start->data<<endl;
}

void pop(){
	head->next = head->next->next;
}

void push(int x){
	node *p = (node *)malloc(sizeof(node));
	p->data = x;
	
	p->next = tail->next;
	tail->next = p;
	tail = p;
	
}

int main()
{
	create(); 
	print(head);
	
	push(100);
	print(head);
	
	pop();
	print(head);
	
	push(101);
	print(head);
} 

```



