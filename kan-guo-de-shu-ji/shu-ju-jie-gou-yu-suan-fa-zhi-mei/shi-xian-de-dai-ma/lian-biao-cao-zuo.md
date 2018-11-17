```
#include<iostream>
#include<stdlib.h>
using namespace std;

typedef struct node{
	int data;
	struct node *next;
}*List;

//建立 
List create()
{
	node *head,*p1;
	head = (node *)malloc(sizeof(node));
	head->next = NULL;
	p1 = head;
	int x;
	while(scanf("%d",&x)!=EOF && x != -1){
		
		node *p2 = (node *)malloc(sizeof(node));
		p2->data = x;
		p2->next = NULL;
		p1->next = p2;
		p1 = p2;
	}
	p1->next = NULL;
	return head;
	
}

//反转 
List reverse(List list)
{
	node *head1,*head2,*p2;
	head1 = list;
	head2 = (node *)malloc(sizeof(node));
	head2->next = NULL;
	p2 = head2;
	for(node* p1=head1->next;p1!=NULL;p1=p1->next){
		
		node* p = (node*)malloc(sizeof(node));
		p->data = p1->data;
		p->next = p2->next;
		p2->next = p;
	}
	return head2;
}


//合并
List merge(List list1,List list2)
{
	node *head3,*head1,*head2,*p1,*p2,*p3;
	p1 = list1->next;
	p2 = list2->next;
	head3 = (node*)malloc(sizeof(node));
	head3->next = NULL;
	p3 = head3;
	while(p1&&p2)
	{
		node *p = (node*)malloc(sizeof(node));
		if(p1->data >= p2->data){ 
			p->data = p2->data;
			p2 = p2->next; 
		}
		else{
			p->data = p1->data;
			p1 = p1->next; 
		}
		p->next = NULL;
		p3->next = p;
		p3 = p;
	}
	
	while(p1)
	{
		node *p = (node*)malloc(sizeof(node));
		p->data = p1->data;
		p->next = NULL;
		p3->next = p;
		p3 = p;
		
		p1 = p1->next; 
	}
	
	while(p2)
	{
		node *p = (node*)malloc(sizeof(node));
		p->data = p2->data;
		p->next = NULL;
		p3->next = p;
		p3 = p;
		
		p2 = p2->next; 
	}
	p3->next = NULL;
	return head3;
}

void print(List list)
{
	for(node* start=list->next;start!=NULL;start=start->next)
		cout<<start->data<<endl;
}

int main()
{
	List list,list1,list2;
	
//	list = create(); 
//	print(list);
	
//	//反转链表
//	//利用头插法
//	//思路:假设有一个头结点，在插入数据的时候每次只插在
//	//头结点后面的位置，这样就可以，构建成一个反转链表 
//	list = reverse(list);
//	print(list);


	list1 = create();
	list2 = create();
	
	//合并 
	list = merge(list1,list2);
	print(list);
	return 0;
	
	//链表中环的检测
	//一个链表中包含环，请找出该链表的环的入口结点
	//思路：通过map来存储每次访问的结点，如果有重复，则是链表入口结点
	
} 

```



