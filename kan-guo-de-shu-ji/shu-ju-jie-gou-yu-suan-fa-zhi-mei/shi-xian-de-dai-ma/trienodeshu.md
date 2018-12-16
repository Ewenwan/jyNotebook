```
#include<iostream>
#include<cstring>
#define MAXN 1000
#define MAX 26
using namespace std;

typedef struct TrieNode{
    char data;
    struct TrieNode *children[MAX];
}TrieNode,*TrieTree;

TrieNode *create()
{
    TrieNode *tree;
    for(int i=0;i<MAX;i++)
    {
        tree->children[i] = NULL;
        tree->data = '/';
    }
    return tree;    
}

void insert(TrieTree &tree,char *s)
{
    int i=0;
    int n = strlen(s);
    TrieNode *p = tree;
    while(i<n)
    {
        int k = s[i] - 'a';
        if(p->children[k] == NULL)
        {
            TrieNode *newNode = create();
            p->children[k] = newNode;
        }
        p = p->children[k];
        p->data = s[i];
    }
}

void search(TrieNode *tree,char *s)
{
    if(tree == NULL)
        return;
    TrieTree p = tree;
    int i = 0;
    int n = strlen(s);
    while(i<n)
    {
        int k = s[i] - 'a';
        if(p->children[k])
            p = p->children[k];
        else
            cout<<endl;
        i++;
    }
    cout<<p->data<<endl;
}

int main()
{
    TrieNode *tree = create();
    char s[MAXN],s1[MAXN];
    cin>>s>>s;
    insert(tree,s);
    search(tree,s1);
    return 0;
}
```



