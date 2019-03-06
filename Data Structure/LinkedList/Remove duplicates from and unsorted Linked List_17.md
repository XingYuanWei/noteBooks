# 17 Remove duplicates from and unsorted Linked List

## Abstract
> 写一个名为removeDupFromUnsorted的方法，从一个无序的Linked List中删去重复的元素。  
> 比如有一个Linked List为：  12->11->12->21->41->43->21。  
> 经过调用removeDuplicates()方法后
> 可以将Linked  List转换为：12->11->21->41->43.


## 思路
* #### 方法一
>有一个很简单也很直接的方法，就是使用两个循环。循环选择选择一个元素，内层循环将剩余的元素一个一个的与外层循环选择出的元素进行比较，
>如果与外层循环的元素相同的话，那么将这个元素删去并释放内存空间。
>代码如下:
```c++
    void removeDupFromUnsortedList(Node * head_ref)
    {
    	    //第一层循环的的引用，第二层循环的引用，要被删去元素的引用
    	    struct Node* outer_ptr, *inner_ptr, *del;
    	    outer_ptr = head_ref;

        //外层循环一个个的选择元素
        while (outer_ptr != NULL && outer_ptr->next != NULL)
        {
        	inner_ptr = outer_ptr;
        	//将选择出的一个元素与Linked List中剩余的元素进行比较
        	while (inner_ptr->next != NULL)
        	{
        		//如果选择出的元素内容与剩余的某个元素内容相同则删去这个
        		//再剩余元素中重复的元素，而不是删去这个被选出的元素
        		if (outer_ptr->data == inner_ptr->next->data)
        		{
        			//以下操作的顺序十分重要不能有错

        			//1.先将重复的元素赋值给del指针
        			del = inner_ptr->next;
        			//2.再把Linked List指针指向 将要被删去元素 的下一个元素
        			inner_ptr->next = inner_ptr->next->next;
        			//3.释放内存
        			//delete(del);
        			free(del);
        			/*
        				补充一下free和delete的区别
        				首先free对应的是malloc；delete对应的是new；
        				free用来释放malloc出来动态内存，
        				delete用来释放new出来的动态内存空间。
        			*/
        		}
        		else
        		{
        			inner_ptr = inner_ptr->next;
        		}
        	}
        	//外层循环指针指向下一个元素
        	outer_ptr = outer_ptr->next;
        }
    }

```

## 方法一的完整代码：

>完整代码
```c++
    #include <cstdio>
    #include <cstdlib>
    #include <iostream>
    #include <cassert>
    
    //添加到Linked List最前
    void push(struct Node** head_ref, int new_data);
    //从指定节点向后打印
    void printList(struct Node* node);
    //从无序Linked List移去重复节点
    void removeDupFromUnsortedList(Node * head_ref);

    struct Node
    {
    	int data;
    	struct Node *next;
    };
    
    int main(){
      struct Node* head = NULL;
      push(&head, 4);
    	push(&head, 13);
    	push(&head, 11);
    	push(&head, 18);
    	push(&head, 11);
    	push(&head, 34);
    	push(&head, 18);
    	push(&head, 11);

    	printf("Linked list before duplicate removal:\n");
    	printList(head);
    	//调用方法
    	removeDupFromUnsortedList(head);
    	
    	printf("Linked list after duplicate removal:\n");
    	printList(head);
    	return 0;
    }
    
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
     
    void removeDupFromUnsortedList(Node * head_ref)
    {
    	//第一层循环的的引用，第二层循环的引用，要被删去元素的引用
    	struct Node* outer_ptr, *inner_ptr, *del;
    	outer_ptr = head_ref;
    	
    	//外层循环一个个的选择元素
    	while (outer_ptr != NULL && outer_ptr->next != NULL)
    	{
    		inner_ptr = outer_ptr;
    		//将选择出的一个元素与Linked List中剩余的元素进行比较
    		while (inner_ptr->next != NULL)
    		{
    			//如果选择出的元素内容与剩余的某个元素内容相同则删去这个
    			//再剩余元素中重复的元素，而不是删去这个被选出的元素
    			if (outer_ptr->data == inner_ptr->next->data)
    			{
    				//以下操作的顺序十分重要不能有错

    				//1.先将重复的元素赋值给del指针
    				del = inner_ptr->next;
    				//2.再把Linked List指针指向 将要被删去元素 的下一个元素
    				inner_ptr->next = inner_ptr->next->next;
    				//3.释放内存
    				//delete(del);
    				free(del);
    				/*
    					补充一下free和delete的区别
    					首先free对应的是malloc；delete对应的是new；
    					free用来释放malloc出来动态内存，
    					delete用来释放new出来的动态内存空间。
    				*/
    			}
    			else
    			{
    				inner_ptr = inner_ptr->next;
    			}
    		}
    		//外层循环指针指向下一个元素
    		outer_ptr = outer_ptr->next;
    	}
    }
   
    //打印链表的内容
    void printList(struct Node* node) {
    	while (node != NULL)
    	{
    		printf("%d\n", node->data);
    		node = node->next;
    	}
    }
```

#### 方法二
> 方法一是最直接简单的方法，但往往这种最直接简单的方法都不是最好的。方法一的Time Complexity为O(n^2)。那么如何时间复杂度降低呢。
> 前面第16篇文章讲述了对一个有序的Linked  List进行去除重复元素，而对有序Linked List进行去除的重复元素的Time Complexity为O()

##### 方法步骤
> 通常而言，归并排序是最合适的排序算法，能够有效的用于对列表进行排序，以下是方法二的操作步骤。
> 1. 对Linked List进行归并排序，通常时间复杂度O(nLogn)
> 2. 移除Linked List中重复的元素，时间复杂度O(n)

#### 方法三
> 我们从头部到尾部遍历Linked List，对于每一个被遍历到的元素，检查它是否已经在Hash Table中，如果在Hash Table中，则移除它。否则，添加到Hash Table中，这个方法的时间复杂度O(n)（假设访问hash table的时间为O(1)）。
> 完整代码如下：

```c++
    #include <cstdio>
    #include <iostream>
    #include <unordered_set>
    #include <cstdlib>

    //打印LinkedList
    void printList(struct Node* n);
    //插入一个新节点在最前面
    void push(struct Node** head_ref, int new_data);
    //delete a element by hash table 
    void removeDupByHashTable(struct Node* head_ref);

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
    	push(&head, 18);
    	push(&head, 11);
    	push(&head, 34);
    	push(&head, 18);
    	push(&head, 11);

    	printf("Linked list before duplicate removal:\n");
    	printList(head);
    	
       removeDupByHashTable(head);

    	printf("Linked list after duplicate removal:\n");
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
    		printf("%d\n", node->data);
    		node = node->next;
    	}
    }
    
    void removeDupByHashTable(Node * head_ref)
    {
    	//用于存储值的集合
    	std::unordered_set<int> hashTable;
    	//对每个元素进行遍历
    	struct Node* current = head_ref;
    	struct Node* prev = NULL;

    	while (current != NULL)
    	{
    		//如果当前的元素已经存储在Hash Table中，则删去这个元素
    		if (hashTable.find(current->data) != hashTable.end())
    		{
    			prev->next = current->next;
    			free(current);
    		}
    		else
    		{
    			//对Hash Table添加一个新的元素
    			hashTable.insert(current->data);
    			//把当前遍历到元素赋给一个prev指针
    			/*

    				if next element will be deleted,so we create a variable named
    				after prev to store current variable.so in if block let prev->next
    				= current->next,
    			*/
    			prev = current;
    		}

    		current = prev->next;
    	}
    }
    
```




