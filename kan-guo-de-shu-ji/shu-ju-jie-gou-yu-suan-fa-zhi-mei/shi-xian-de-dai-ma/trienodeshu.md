```
#include<iostream>
#include<cstring>
#include<cstdlib>
#include<queue> 
#define MAXN 1000
#define MAX 26
using namespace std;

struct TrieNode{
	int count;
	TrieNode *fail;
	TrieNode *next[MAX];
	TrieNode()
	{
		for(int i=0;i<26;i++)
			next[i] = NULL;
		fail = NULL;
		count = 0;
	}
}*root;

void insert(char s[])
{
	int length = strlen(s);
	TrieNode *p = root;
	for(int i=0;i<length;i++)
	{
		if(p->next[s[i]-'a'] == NULL)
			p->next[s[i]-'a'] = new TrieNode();
		p = p->next[s[i]-'a'];
	}
	p->count++;
}

void bfs()
{
	queue<TrieNode*>que;
	que.push(root);
	while(!que.empty())
	{
		TrieNode *q = que.front();
		que.pop();
		for(int i=0;i<26;i++)
		{
			if(q->next[i] != NULL)
			{
				if(q == root)
					q->next[i]->fail = root;
				else
				{
					TrieNode *p = q->fail;
					while(p)
					{
						if(p->next[i])
						{
							q->next[i]->fail = p->next[i];
							break;
						}
						p = p->fail;
					}
					if(p == NULL)
						q->next[i]->fail = root;
				}
				que.push(q->next[i]);
			}
		}
	}
}


int query(char s[])
{
	int sum=0,i=0;
	TrieNode *p = root;
	while(s[i])
	{
		int pos = s[i] - 'a';
		while(p->next[pos] == NULL && p != root)
			p = p->fail;
		p = p->next[pos];
		if(!p)
			p = root;
		TrieNode* t = p;
		while(t != root)
		{
			if(t->count >= 0)
			{
				sum += t->count;
				t->count = -1;
			}
			else
				break;
			t = t->fail;
		}
		i++;
	}
	return sum;
}

int main()
{
	int n;
	root = new TrieNode();
	cin>>n;
	for(int i=0;i<n;i++)
	{
		char s[MAXN];
		cin>>s;
		insert(s);
	}
	bfs();
	char s1[MAXN];
	cin>>s1;
	int ans = query(s1);
	cout<<ans<<endl;
	return 0;
}
// 5 she he say shr her 
// yasherhs
// 3
// 3个单词匹配 
```



