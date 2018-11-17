```
#include<iostream>     
#include<stack>     
#include<string>     
#include<cctype>
#include<stdlib.h>
using namespace std;    

typedef string::size_type it;    

char Compare(char op,char ch)    //优先级比较     
{    
    if((op=='#'&&ch=='#')||(op=='('&&ch==')')) return '=';    
    if(ch=='#') return '<';    
    if(op=='#') return '>';    
    if(op=='(') return '>';    
    if(ch==')') return '<';    
    if(ch=='(') return '>';    
    if(ch=='*'||ch=='/')     
    if(op=='+'||op=='-') return '>';    
    else return '<';    
    if(ch=='+'||ch=='-') return '<';    
}    

void modify(string& s)   //优化表达式      
{    
    string s1="()+-*/";    
    for(it i=0;i<s.size();++i)    
    {    
        if(isspace(s[i])) s.erase(i,1);    
        if(!isdigit(s[i])&&s[i]!='.'&&s1.find(s[i])==string::npos) s.erase(i,1);    
        if(s[i]=='('&&s[i+1]=='-') s.insert(i+1,"0");    
        if(i==0&&s[i]=='-') s.insert(i,"0");    
    }    
}    

bool check(const string & s)    //检验输入表达式      
{    
    string s1="()+-*/";    
    string s2="+-*/";     
    stack<char> ch;    
    bool valid=true;    
    for(it i=0;i<s.size();++i)    
    {    
        if(i==0 && s1.find(s[i],1)!=string::npos) return false;    
        switch(s[i])    
        {    
        case '(':     
            if(s1.find(s[i+1],1)!=string::npos) return false; break;     
        case ')':    
            if(s2.find(s[i-1])!=string::npos) return false; break;    
        case '+':    
        case '-':    
        case '*':    
        case '/':    
            if(s2.find(s[i+1])!=string::npos) return false; break;     
        }    
        if (s[i]=='(') ch.push(s[i]);    
        if (s[i]==')')    
            if (ch.empty())     
            {    
                valid=false;    
                break;    
            }    
            else    
            {    
                char b=ch.top(); ch.pop();    
                if (b=='(') valid=true;    
                else valid=false;    
            }    
    }    
    if (!ch.empty()) valid=false;    
    return valid;    
}    

void Calculate(stack<double>& num,stack<char>& ops,const string & s)    
{    
    string s1="()+-*/#";    
    it i=0;    
    while(i<s.size())    
    {    
        it j=s.find_first_of(s1,i);    
        if(j!=string::npos)    
        {    
            if(j!=i)    
            {    
                string s2=s.substr(i,j-i);    
                double n=atof(s2.c_str());    
                num.push(n);    
            }    
            char ch=s[j];    
            char op=ops.top();    
            if(Compare(op,ch)=='>') ops.push(ch);    
            else if(Compare(op,ch)=='=') ops.pop();    
            else     
            {    
                while(1)    
                {    
                    char c=ops.top();    
                    if(Compare(c,ch)=='>') { ops.push(ch); break; }    
                    else if(Compare(c,ch)=='=') { ops.pop(); break; }    
                    else     
                    {    
                        char optr=ops.top();    
                        ops.pop();    
                        double n1=num.top();    
                        num.pop();    
                        double n2=num.top();    
                        num.pop();    
                        double value;    
                        if(optr=='+') value=n2+n1;    
                        if(optr=='-') value=n2-n1;    
                        if(optr=='*') value=n2*n1;    
                        if(optr=='/')     
                        {    
                            double E=0.00001;    
                            if( n1>-E && n1<E )    
                            {    
                                cout<<"Can't evaluate the expression !";    
                                exit(1);    
                            }    
                            else value=n2/n1;    
                        }    
                        num.push(value);    
                    }    
                }    
            }    
        }    
        i=j+1;  //更新i的值      
    }    
}     
int main()    
{    
    stack <double> num;    
    stack <char> ops;    
    ops.push('#');    
    string s;  

    cout<<"Input the string:"<<endl;    
    getline(cin,s);    
    modify(s);    
    while(!check(s))     
    {    
        cout<<"The string is not valid. Input it again! "<<endl;    
        getline(cin,s);    
        modify(s);    
    }    
    cout<<s<<endl; 
    s=s+"#";    

    Calculate(num,ops,s);    
    cout<<"The result is "<<num.top();    

    return 0;    
}
```



