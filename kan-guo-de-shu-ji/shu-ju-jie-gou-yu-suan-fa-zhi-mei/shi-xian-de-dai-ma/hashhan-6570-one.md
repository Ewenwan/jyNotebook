```
#include<iostream>
#include<string>
#include<map>

using namespace std;

map<int,string>a;

int hash_op(string key)
{
    //获取后两位字符
    string lastTwoChars = key.substr(key.length()-2,key.length());
    //将后两位字符转换为整数
    int hashValue =  stoi(lastTwoChars);
    return hashValue;
}



int main()
{
    string key;
    while(true)
    {
        cin>>key;
        int hash_key = hash_op(key);
        if(a.count(hash_key))
        {
            cout<<"重复hash值"<<endl;
        }
        else
        {
            a[hash_key] = key;
            cout<<hash_key<<":"<<a[hash_key]<<endl;
        }
    }
    return 0;
}
```

```
#include<iostream>
#include<string>
#include<map>

using namespace std;

map<int,string>a;

int hash_op(string key)
{
	int result = stoi(key)%10;
	return result;
}

int next_hash(int key)
{
	if(a.count(key))
		next_hash(key+1);
	else
		return key;
} 

int main()
{
	string key;
	while(true)
	{
		cin>>key;
		int hash_key = hash_op(key);
		if(a.count(hash_key) && a[hash_key]!=key )
		{
			hash_key = next_hash(hash_key+1);
			a[hash_key] = key;
			cout<<hash_key<<":"<<a[hash_key]<<endl;
		}
		else
		{
			a[hash_key] = key;
			cout<<hash_key<<":"<<a[hash_key]<<endl;
		}
	}
	return 0;
} 
```



