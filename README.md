# Balanced_Parantheses
#include<iostream>
#include<string>
#include<algorithm>
#include<vector>
#include<cmath>
using namespace std;

template <class t>
class Stack
{
private:
	struct Node
	{
		t item;
		Node* next;
	};
	Node* top;

public:
	Stack()
	{
		top = NULL;
	}

	bool IsEmpty();
	void PUSH(t newItem);
	void POP();
	void GetStack(t &x);
	void display();
};

template <class t>
void Stack<t>::PUSH(t newItem)
{
	Node* newItemPTR = new Node;
	if (newItemPTR == NULL)
	{
		cout << "ERROR IN MEMORY TO PUSK IN STACK" << endl;
	}

	else
	{
		newItemPTR->item = newItem;
		newItemPTR->next = top;
		top = newItemPTR;
	}
}

template <class t>
bool Stack<t>::IsEmpty()
{
	if (top == NULL)return true;
	else return false;
}


template <class t>
void Stack<t>::POP()
{

	if (IsEmpty())
	{
		cout << "THE STACK IS EMPTY!" << endl;
	}
	else
	{
		Node* temb;
		temb = top;
		top = top->next;
		temb = temb->next = NULL;
		delete temb;
	}
}

template <class t>
void Stack<t>::GetStack(t& x)
{
	if (IsEmpty())
	{
		cout << "ERROR" << endl;
	}
	else
	{
		x = top->item;
	}
}

template<class t>
void Stack<t>::display()
{
	Node* cur;
	cur = top;
	cout << "THE ITEMS IN THE STACK ARE : ";
	cout << "[ ";
	while (cur != NULL)
	{
		cout << cur->item << " ";
		cur = cur->next;
	}
	cout << " ]" << endl;
}



template <class t>
class Balanded_Parenthese
{
public:
	
	bool ArePair(char open, char closed)
	{
		if (open == '(' && closed == ')')return true;
		else if (open == '{' && closed == '}')return true;
		else if (open == '[' && closed == ']')return true;
		else return false;
	}
	
	
	bool AreBalansed(string exp)
	{
		Stack<char> st;

		for (int i = 0; i < exp.size(); i++)
		{
			char c = exp[i];

			if (c == '(' || c == '{' || c == '[')
			{
				st.PUSH(c);
			}

			else if (c == ')' || c == '}' || c == ']')
			{
				char top;

				if (st.IsEmpty())
					return false;

				st.GetStack(top);

				if (!ArePair(top, c))
					return false;

				st.POP();
			}
		}

		return st.IsEmpty();
	}
};






int main()
{
	Balanded_Parenthese<char> obj;

	string s;
	cin >> s;

	if (obj.AreBalansed(s))
		cout << "Balanced";
	else
		cout << "Not Balanced";
}



