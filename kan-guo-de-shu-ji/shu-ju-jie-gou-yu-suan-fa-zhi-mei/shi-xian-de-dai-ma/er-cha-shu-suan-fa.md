```
#include<iostream>
#include<cstdlib>
#include<queue>
#include<algorithm>
using namespace std;

typedef struct Tree{
	char data;
	struct Tree *left;
	struct Tree *right;
}Tree,*TreeNode;

//建立
//输入:ABD##E##CF##G## 
void Create(TreeNode &tree)
{
	char ch;
	scanf("%c",&ch);
	if(ch == '#')
		tree = NULL;
	else{
		tree = (TreeNode)malloc(sizeof(struct Tree));
		tree->data = ch;
		Create(tree->left);
		Create(tree->right);
	}
}

//前序遍历
//输出:ABDECFG 
void preOrder(TreeNode &tree)
{
	if(tree == NULL) return;
	cout<<tree->data;
	preOrder(tree->left);
	preOrder(tree->right);
}

//中序遍历
//输出:DBEAFCG
void inOrder(TreeNode &tree)
{
	if(tree == NULL) return;
	inOrder(tree->left);
	cout<<tree->data;
	inOrder(tree->right);
} 

//后续遍历
//输出:DEBFGCA
void postOrder(TreeNode &tree)
{
	if(tree == NULL) return;
	postOrder(tree->left);
	postOrder(tree->right);
	cout<<tree->data;
}

//层次遍历
//输出:ABDECFG
void levelOrder(TreeNode &tree)
{
	queue<TreeNode>q;
	if(tree == NULL) return ;
	q.push(tree);
	while(!q.empty())
	{
		TreeNode p = q.front();
		q.pop();
		cout<<p->data;
		if(p->left)
			q.push(p->left);
		if(p->right)
			q.push(p->right);
	}
}

int high(TreeNode tree)
{
	if(tree == NULL)
		return 0;
	else
		return max(high(tree->left),high(tree->right))+1;
}

int main()
{
	TreeNode tree;
	Create(tree);
	cout<<"前序遍历:"; 
	preOrder(tree);
	cout<<endl;
	cout<<"中序遍历:";
	inOrder(tree);
	cout<<endl;
	cout<<"后序遍历:";
	postOrder(tree);
	cout<<endl;
	cout<<"层次遍历:";
	levelOrder(tree);
	
	cout<<endl;
	cout<<high(tree)<<endl;
	return 0;
} 
```



