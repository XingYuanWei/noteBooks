# Swap nodes without swapping data 


## Abstract
> 给定两个一个Linked List和存在于Linked List中的两个值，应该交换节点，而不是节点中数据，因为当有很多值的情况下，如果此时交换节点可能花费比较  
> 昂贵的代价。可以先假设Linked List中的所有值都是不同的。
> 例如：
> 
    Input:  10->15->12->13->20->14,  x = 12, y = 20 
    Output: 10->15->20->13->12->14
    Input:  10->15->12->13->20->14,  x = 10, y = 20
    Output: 20->15->12->13->10->14
    Input:  10->15->12->13->20->14,  x = 12, y = 13
    Output: 10->15->13->12->20->14


> 这看起来似乎是一个很简单的问题，但是的有以下的几个问题要处理。在接下来的叙述中，用x和y表示要交换的两个元素。
> * x和y可能不是毗邻的两个元素
> * x和y俩者之中可能是头节点
> * x和y俩者之中可能是尾节点
> * x和y俩者之中可以不在Linked List中，也可能都不在。  
> 如何只用精简的代码优雅的解决上面那些可能出现问题。
> 完整代码如下：

```c++
    #include <cstdio>
    #include <iostream>
    #include <unordered_set>
    #include <cstdlib>

    //print LinkedList's content
    void printList(struct Node* n);
    //插入一个新节点在最前面
    void push(struct Node** head_ref, int new_data);
    //swap two nodes
    void swapTwoNodes(struct Node**,int,int);

    struct Node
    {
    	int data;
    	struct Node *next;
    };


    int main() {

    	/* Start with the empty list */
    	struct Node* head = NULL;

    	/* Let us create a sorted linked list to test the functions
    	 Created linked list will be 11->11->11->13->13->20 */
    	push(&head, 4);
    	push(&head, 13);
    	push(&head, 11);
    	push(&head, 34);
    	push(&head, 18);

    	printf("Linked list before :");
    	printList(head);
    	printf("\n");

    	swapTwoNodes(&head, 4, 34);


    	printf("\n");
    	printf("Linked list after :");
    	printList(head);

    	return 0;

    }

    //add a new node in the head
    void push(struct Node** head_ref, int new_data) {
    	//1.allocate node
    	struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    	//2. put in the data;
    	new_node->data = new_data;
    	//3.make next of new node as head
    	new_node->next = *head_ref;
    	//4.move the head to point to the new node;
    	*head_ref = new_node;
    }

    //print linked list content
    void printList(struct Node* node) {
    	while (node != NULL)
    	{
    		printf("%d->", node->data);
    		node = node->next;
    	}
    }

    void swapTwoNodes(Node ** head_ref, int x, int y)
    {
    	//Nothing to do if x and y are same
    	if (x == y) {
    		std::cout << "the nodes are same!" << std::endl;
    		return;
    	}

    	//search for x(keep track previous of x )
    	struct Node *prevX = NULL, *currX = *head_ref;
    	//stop loop when currX is NULL and currX->data not equal x
    	//and record currX regard as prevX
    	while (currX && currX->data != x)
    	{
    		prevX = currX;
    		currX = currX->next;
    	}
    	//taverse y as long as traverse x
    	struct Node *prevY = NULL, *currY = *head_ref;
    	while (currY && currY->data != y)
    	{
    		prevY = currY;
    		currY = currY->next;
    	}

    	//if either x or y is not present,nothing to do 
    	if (currX == NULL || currY == NULL)
    	{
    		std::cout << "either x or y is not present!" << std::endl;
    		return;
    	}

    	//if prevX not equal NULL,it stand for the x is not head of Linked list
    	if (prevX != NULL)
    	{
    		prevX->next = currY;
    	}
    	else //else make y as new head
    	{
    		*head_ref = currY;
    	}

    	//like X
    	if (prevY != NULL)
    	{
    		prevY->next = currX;
    	}
    	else //else make x as new head
    	{
    		*head_ref = currX;
    	}

    	struct Node *temp = currY->next;
    	currY->next = currX->next;
    	currX->next = temp;
    }
```

## 分析
#### 画图解释

