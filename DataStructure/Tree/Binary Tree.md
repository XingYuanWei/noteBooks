# Binary Tree


## Abstract
>不像数组还有链表，栈和队列，这样的线性结构，树是一种分层的数据结构。


## 树的特点
>1. 树提供一些折中的访问数据和搜索数据方法，速度比链表快但是比数组慢。
>2. 树提供了折中的插入和删除方法，速度比数组快但是比链表慢。
>3. 像链表一样，树的节点的个数没有上限，节点与节点也是使用指针进行连接


## 树包括了哪些应用
>1. 操作层间的数据 
>2. 使得信息更容易的搜索
>3. 保持数据的排序状态
>4. 工作流程使得层次分明，更有结构化
>5. 路由算法
>6. 多阶段决策


## 二叉树
>一种最多只有两个节点的数，因为每个二叉树中只能有两个节点，所以我们很形象的称两个节点为左节点和右节点



## C语言实现二叉树
>在C语言中用四个节点创建一个简单的树，创建的树如下图
>
>         tree
>         ----
>          1    <-- root
>        /   \
>       2     3  
>      /   
>     4  
> 

```c++  
    #include<iostream>
    #include<cstdlib>

    struct node
    {
    	int data;
    	struct node* left;
    	struct node* right;
    };

    /*
    	newNode() allocates a new node with the data and NULL left 
    	and right pointers
    */

    struct node* newNode(int data)
    {
    	
    	//allocate memory for new node
    	struct node* node = (struct node*)malloc(sizeof(struct node));
    	 
    	//assign data to this node
    	node->data = data;

    	//Initialize left and right children as NULL
    	node->right = NULL;
    	node->left = NULL;
    	return node;
    };


    int main() {

    	//create root
    	struct node* root = newNode(1);

    	/* following is the tree after above statement
    		   1
    		 /   \
    		NULL  NULL
    	*/

    	root->left = newNode(2);
    	root->right = newNode(3);
    	/* 2 and 3 become left and right children of 1
    			   1
    			 /   \
    			2      3
    		 /    \    /  \
    		NULL NULL NULL NULL
    	*/

    	root->left->left = newNode(4);
    	/* 4 becomes left child of 2
    				  1
    			  /       \
    			 2          3
    		   /   \       /  \
    		  4    NULL  NULL  NULL
    		 /  \
    		NULL NULL
    	*/
    	return 0;
}
```

## 总结
> 树是一个层的数据结构，主要用于维护想树一样的层级结构，提供中等的访问、插入、删除等操作。二叉树
> 是最多只有两个子节点的一种特殊的树。
