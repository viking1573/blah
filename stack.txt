#include <iostream>
using namespace std;
template <typename T> class Stack
{
	Stack *top;
	T a,b;
	char x;
	Stack *next;
	Stack *newnode;
	public:
		Stack()
		{
		top=NULL;
		}
		T data;
		void push(T b);
		void pop();
		void infixtopostfix(char[],char[]);
		int priority (char);
		Stack <T>* createnode(T);
		void reversestr(char [],char []);
		void infixtoprefix(char[],char[],char[],char[]);
		void evalpostfix(char[],char[],float[]);
		void evalprefix(char[],char[],char[],char[],float[]);
};

template <typename T> Stack <T>* Stack<T> :: createnode (T a)
{
Stack <T>* newnode =new Stack ();
newnode -> data=a;
newnode -> next=NULL;
return newnode;
}
template <typename T>void Stack<T>:: push(T b)
{
Stack <T>* newnode = createnode (b);
if (top==NULL)
{
top=newnode;
}
else
{
newnode->next=top;
top=newnode;
}
}
template <typename T>void Stack<T>:: pop()
{
Stack *ptr;
if (top==NULL)
{
cout<<"Stack is empty";
}
else
{
ptr=top;
top=top->next;
ptr->next=NULL;
delete (ptr);
}
}
template <typename T> int Stack<T> :: priority(char x)
{
if (x=='/' || x=='*')
return 3;
else if (x=='+' || x=='-')
return 2;
else
return 1;
}
template<typename T> void Stack <T> :: reversestr(char infix[15],char revinfix[15])
{
int len;
int i=0;
int j;
while(infix[i]!='\0')
{
i++;
}
len=i;
i--;
for( j=0;j<len;j++)
{
if(infix[i]=='(')
revinfix[j]=')';
else if(infix[i]==')')
revinfix[j]='(';
else
revinfix[j]=infix[i];
i--;
}
revinfix[j]='\0';
}
template<typename T> void Stack <T> :: infixtopostfix(char infix [15], char postfix [15])
{
int i=0,j=0;
while(infix[i]!='\0')
{
if(! isalnum(infix[i]))
{
if (top==NULL)
push(infix[i]);
else if (infix[i]=='(')
push(infix[i]);
else if (infix[i]==')')
{
while(top->data !='(')
{
postfix[j]=top->data;
pop();
j++;
}
pop();
}
else
{
while (priority(infix[i])<=priority(top->data))
{
postfix[j]=top->data;
pop();
j++;
if (top==NULL)
break;
}
push (infix[i]);
}
}
else
{
postfix[j]=infix[i];
j++;
}
i++;
}
while(top!=NULL)
{
postfix[j]=top->data;
pop();
j++;
}
postfix[j]='\0';
}
template<typename T> void Stack <T> :: infixtoprefix (char infix[15],char postfix[15],char
revinfix[15],char prefix[15])
{
reversestr(infix,revinfix);
infixtopostfix(revinfix,postfix);
reversestr(postfix,prefix);
}
template<typename T> void Stack <T> :: evalpostfix (char postfix[15],char infix[15],float
eval[15])
{
int i=0;
float result;
float result1;
infixtopostfix(infix,postfix);
while(postfix[i]!='\0')
{
if(isalpha(postfix[i]))
{
cout<<"Enter the value for "<<postfix[i]<<" "<<":"<<" ";
cin>>eval[i];
push(eval[i]);
}
else
{
float x=top->data;
pop();
float y=top->data;
pop();
if(postfix[i]=='+')
result=y+x;
if(postfix[i]=='-')
result=y-x;
if(postfix[i]=='*')
result=y*x;
if(postfix[i]=='/')
result=y/x;
push(result);
}
i++;
}
result1=top->data;
cout<<"The result after evaluation is: "<<result1<<"\n";
}
template<typename T> void Stack <T> :: evalprefix (char infix[15],char postfix[15],char
revinfix[15],char prefix[15],float eval[15])
{
int i=0;
float result;
float result1;
infixtoprefix(infix,postfix,revinfix,prefix);
while(prefix[i]!='\0')
{
i++;
}
i--;
while(i>=0)
{
if(isalpha(prefix[i]))
{
cout<<"Enter the value for :"<<prefix[i]<<" ";
cin>>eval[i];
push(eval[i]);
}
else
{
float x=top->data;
pop();
float y=top->data;
pop();
if(prefix[i]=='+')
result=x+y;
if(prefix[i]=='-')
result=x-y;
if(prefix[i]=='*')
result=x*y;
if(prefix[i]=='/')
result=x/y;
push(result);
}
i--;
}
result1=top->data;
cout<<"The value after prefix expression is : "<<result1<<"\n";
}
int main()
{
int num1;
Stack <char> s1;
Stack <char> s2;
char infix[15];
char postfix[15];
float eval[15];
char revinfix[15];
char prefix[15];
cout<<"Enter infix expression : ";
cin>>infix;
do{
int num;
cout<<"Enter operation to be performed : "<<"\n"<<"1. Conversion to postfix "<<"\n"<<"2.Conversion to prefix "<<"\n"<<"3.Evaluation of postfix"<<"\n"<<"4.Evaluation of prefix "<<"\n";
cin>>num;
switch(num)
{
case 1:
s1.infixtopostfix(infix,postfix);
cout<<"The postfix expression is : "<<postfix<<"\n";
break;
case 2:
s1.infixtoprefix(infix,postfix,revinfix,prefix);
cout<<"The prefix expression is : "<<prefix<<"\n";
break;
case 3:
s1.evalpostfix(postfix,infix,eval);
break;
case 4:
s2.evalprefix(infix,postfix,revinfix,prefix,eval);
break;
}
cout<<"Do you want to continue?"<<"\n"<<"1. Yes or 2. No"<<"\n";
cin>>num1;
}while(num1!=2);
}

