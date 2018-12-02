```
#include<iostream>
#include<cstdlib>
#include<queue>
using namespace std;

typedef struct Tree{
	int data;
	struct Tree *left;
	struct Tree *right;
}Tree,*TreeNode;

typedef int Elemtype;

void insert(TreeNode &tree,int data)
{
	if(tree == NULL)
	{
		tree = (TreeNode)malloc(sizeof(Tree));
		tree->left = NULL;
		tree->right = NULL;
		tree->data = data;
		return;
	}
	if(data < tree->data)
		insert(tree->left,data);
	else if(data > tree->data)
		 insert(tree->right,data);
	else
		cout<<"已经存在了"<<endl;
	
}

//中序遍历
void inOrder(TreeNode &tree)
{
	if(tree == NULL) return;
	inOrder(tree->left);
	cout<<tree->data<<" ";
	inOrder(tree->right);
} 

bool find(TreeNode tree,int data)
{
	if(tree != NULL)
	{
		if(data == tree->data)
			cout<<"找到了"<<endl;
		else if(data > tree->data)
			find(tree->right,data);
		else
			find(tree->left,data);
		return 1;
	}
	else{
		cout<<"没找到"<<endl;
		return 0;
	}
}


TreeNode findMin(TreeNode tree)
{
	if(tree->left == NULL)
		return tree;
	else
		findMin(tree->left);
}

TreeNode findMax(TreeNode tree)
{
	if(tree->right == NULL)
		return tree;
	else
		findMin(tree->right);
}

TreeNode findPre(TreeNode tree,int data)
{
	if(tree->data!=data && (tree->left || tree->right))
	{
		if(data == tree->left->data || data == tree->right->data)
		{
			cout<<"找到了"<<endl;
			return tree;
		}
		if(data > tree->data)
			findPre(tree->right,data);
		if(data < tree->data)
			findPre(tree->left,data);
	}
	else{
		cout<<"没有前驱"<<endl;
		return NULL;
	}
}

void del(TreeNode &tree,int data)
{
	if(tree == NULL)
		return ;
	if(tree->data > data)
		del(tree->left,data);
	else if(tree->data < data)
		del(tree->right,data);
	else
	{
		if(tree->left && tree->right)
		{
			TreeNode p = tree->right;
			TreeNode root = tree;
			
			while(p->left != NULL)
			{
				root = p;
				p = p->left;
			}
			tree->data = p->data;
			p = NULL;
		}
		else if(tree->left || tree->right)
		 	if(tree->left)
		 		tree = tree->left;
		 	else
		 		tree = tree->right;
		else
		{
			tree = NULL;
		}
	}
}

int main()
{
	TreeNode tree;
	int a[] =  {45,24,53,12,24,90,4,1};
	for(int i=0;i<sizeof(a)/sizeof(a[0]);i++)
		insert(tree,a[i]);
	inOrder(tree);
	cout<<endl;
	find(tree,12);
	insert(tree,100);
	inOrder(tree);
	cout<<endl;
	
	cout<<"最小值:";
	cout<<findMin(tree)->data<<endl;
	
	del(tree,1);
	del(tree,4);
	del(tree,100);
	inOrder(tree);
	
	cout<<endl;
	cout<<"前驱结点:";
	cout<<findPre(tree,24)->data<<endl;
	return 0;
}
```



