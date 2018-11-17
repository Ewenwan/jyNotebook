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
int length=0;

LinkedList create()
{
	Node *tail,*head,*pre;
	head = (Node *)malloc(sizeof(Node));
	head->next=head->pre=head;
	//尾巴与头相接，形成循环 
	tail = head->next;
	while(scanf("%d",&value)!=EOF && value != -1)
	{
		length++;
		Node *p = (Node *)malloc(sizeof(Node));
		p->data = value;
		p->pre = tail;
		tail->next = p;
		tail = p;
	} 
	//头尾相接 ，双向循环 
	tail->next = head;
	head->pre = tail;
	return head;
}



void print(LinkedList head)
{
	int n=0; 
	Node *p=head->next;
	while(p&&length>0)
	{
		//注意head没使用头结点，跳过 
		if(p!=head)
		{
			n++;
			if(n%3==0)
			{
				cout<<p->data<<endl;
				//删除，将p节点上下的节点联系起来 
				p->pre->next = p->next;
				p->next->pre = p->pre;
				length--;
			}
		}
		p=p->next;
	}
}

int main()
{
	LinkedList list;
	list = create();
	print(list);
	return 0;
} 

```



