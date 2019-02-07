# Stack Data Structure

## Abstract

> 栈是一种线性的数据结构，它有着特殊的操作和运行方式。其顺序是FILO(First In Last Out)。现实生活中有许多事物就像栈一样，
> 比如食堂中堆叠的盘子，放在最顶层的盘子是最先被拿走，而在最底层的一个盘子将会保留最长时间最后被拿走。或者可以把栈
> 看作一个羽毛球筒，打开盖子后最底下的一个羽毛球是第一个放入，但是如果要拿出的话则是最后一个拿出。
>栈中主要有执行以下几种基本操作。

#### ① Push：添加一个项目在栈中。如果栈已满，则称之为溢出条件。
#### ② Pop：移除栈顶的项目。如果栈是空的，则称之为下溢条件。
#### ③ Peek or Top：返回栈中最顶层的元素。
#### ④ isEmpty：如果栈为空则返回真，否则返回假。

>push，pop，isEmpty，peek这些操作的时间复杂度都为O(1)，这些操作我们不需要做任何的循环。
>栈的实现有两种方式，第一种为使用数组，第二种为使用Linked List。下面代码使用的是Array。


```c++
    #include <iostream>

    using namespace std;

    #define MAX 10000

    class Stack
    {
    public:
    	int a[MAX];
    	Stack();
    	~Stack();
    	int pop();
    	bool push(int x);
    	bool isEmpty();

    private:
    	int top;
    };

    Stack::Stack()
    {
    	top = -1;
    }

    Stack::~Stack()
    {
    }

    int Stack::pop()
    {
    	if (top < 0)
    	{
    		cout << "Stack Underflow" ;
    		return false;
    	}
    	else
    	{
    		int x = a[top--];
    		return x;
    	}
    }

    bool Stack::push(int x)
    {
    	if (top >= (MAX - 1))
    	{
    		cout << "Stack Overflow";
    		return false;
    	}
    	else
    	{
    		a[++top] = x;
    		cout << x << "push into stack\n";
    		return true;
    	}
    }

    bool Stack::isEmpty()
    {
    	return top < 0;
    }


    int main() {
    	class Stack stack;
    	stack.push(10);
    	stack.push(20);
    	stack.push(30);
    	cout << stack.pop() << "popped from stack\n";
    	return 0;
    }
```

