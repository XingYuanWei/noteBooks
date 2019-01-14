# Linked List Insertion_4



## Abstract 
> 此文在上篇文章的基础上讲述如何在一个Linked List中插入一个节点。插入一个节点，可以有三种的插入方式。  
> * 在链表头部中插入
> * 在链表尾部中插入
> * 插入到给定的某个节点的后面  
> 下面将依次介绍这三种方法



## 1.插入到链表的投头部
>一个新的节点常常都会添加到给定Linked List的头部中，使得新加入的节点变成了Linked List中的新的头结点。例如
>10->15->20->25，我们添加一个新节点5在10的前面，这样链表的顺序就变成了5->10->15->20->25。我们常常把这样
>添加新节点在头部的方法称为push()。这个push()方法需要接收一个Linked List的头指针。下图所示的就是添加一个新节点E
>到A的前面，使得E变成了Linked List的头结点。如图：
>
>![添加新节点到头部](_v_images/20190114223904884_314.png)
>push一个节点需要4步骤
>### ① 分配一个新节点的内存空间
>### ② 输入数据
>### ③ 将新节点的next指向原来的头节点
>### ④ 移动头指针使得头指针指向新节点
>push方法的代码如下所示：
```c++
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
```

### 完整的代码如下所示
```c++
    #include <cstdio>
    #include <iostream>
    #include <unordered_set>
    #include <cstdlib>

    //print LinkedList's content
    void printList(struct Node* n);
    //插入一个新节点在最前面
    void push(struct Node** head_ref, int new_data);


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
    	push(&head, 7);
    	push(&head, 6);
    	push(&head, 5);
    	push(&head, 4);
    	push(&head, 3);
    	push(&head, 2);
    	push(&head, 1);

    	printf("Linked list before :");
    	printList(head);
    	printf("\n");


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
```
