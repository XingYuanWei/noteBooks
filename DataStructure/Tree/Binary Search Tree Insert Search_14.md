# Binary Search Tree_14


## Abstract 
> 二叉搜索树，是一个基于二叉树的数据结构，有着如下性质的树。
> 1. 若左子树非空，其左子树的任何节点关键字均小于根节点的关键字
> 2. 若右子树非空，则右子树上所有节点关键字均大于根节点的关键字
> 3. 左右子树也是二叉排序树  
> 4. 节点键值也不能有重复的

![二叉搜索树](_v_images/20190508091327670_29782.png)


> 在上面的几个性质下，二叉搜索树保持节点与节点之间有着一定的顺序，这样使得像搜索，最大值，最小值这样的
> 操作速度变快，如果是没有按照上述的顺序，可能就要比较给定的每一个节点。


## 插入一个键
> 始终在叶子节点处插入新键。我们从root开始，
> 直到我们到达一个叶子节点。找到叶子节点后，
> 新节点将添加为叶子节点的子节点。
> 
         100                               100
        /   \        Insert 40            /    \
      20     500    --------->          20     500 
     /  \                              /  \  
    10   30                           10   30
                                              \   
                                              40
> 1. 从root节点开始
> 2. 与根节点比较插入的元素，如果小于root节点，递归比较左子树的节点，否则递归比较右子树
> 3. 查找节点后插入左边，否则插入右边。
> 
![BST中插入节点 ](_v_images/20190508091048421_2218.png)


## 查找一个键
> 在二叉搜索树中查找一个给定的键，
> 1. 首先把他和root节点比较，如果是root节点，则返回root节点
> 2. 如果键的值比root节点更大，递归的查找根节点的右子树，否则递归的查找左节点。
> 3. 如果在某个节点找到元素，则返回该节点，否则返回NULL。


## BST中插入节点和查找节点的C++代码
```c++
    // C++ program to demostrate insert and search operation in BST

    #include <iostream>
    #include <cstdlib>

    using namespace std;

    struct node {
    	int key;
    	struct node* left, * right;
    };

    struct node* newNode(int item) {
    	struct node* newNode = (struct node*)malloc(sizeof(struct node));
    	newNode->key = item;
    	newNode->left = NULL;
    	newNode->right = NULL;
    	return newNode;
    }

    //中序遍历
    void inorder(struct node* root) {
    	if (root != NULL) {
    		inorder(root->left);
    		cout << endl << root->key;
    		inorder(root->right);
    	}
    }

    //insert a node in BST
    struct node* insert(struct node* node, int key) {
    	//树如果是空的 返回一个节点即为root节点
    	if (node == NULL) return newNode(key);
    	// 如果将要插入的键值小于节点的值 则递归到左边，否则右边
    	if (key < node->key) {
    		node->left = insert(node->left, key);
    	}
    	else if(key > node->key)
    	{
    		node->right = insert(node->right, key);
    	}
    	return node;
    }


    //search a node
    struct node* search(struct node* root, int key) {
    	if (root == NULL || root->key == key) {
    		return root;
    	}
    	//如果要查找的键大于根，则去右子树查找
    	if (key > root->key) {
    		return search(root->right, key);
    	}
    	return search(root->left, key);
    }

    int main() {
    	/* Let us create following BST
    			  50
    		   /     \
    		  30      70
    		 /  \    /  \
    	   20   40  60   80 */
    	struct node* root = NULL;
    	root = insert(root,50);
    	insert(root, 30);
    	insert(root, 20);
    	insert(root, 40);
    	insert(root, 70);
    	insert(root, 60);
    	insert(root, 80);

    	// print inoder traversal of the BST 
    	inorder(root);

    	cout << endl << "search 40:";
    	struct node* searchNode = search(root, 40);
    	cout << searchNode->key;

    	return 0;
    }


```
## 时间复杂度
>对于插入和搜索操作，时间复杂度为O(h),其中h是BST的高，最坏的情况下，我们可能要从root节点遍历到
>最深的叶子节点，倾斜树的高度可能变为n，搜索和插入操作的时间复杂度可能变为O（n）。



## 结果
![插入节点和查找节点的结果](_v_images/20190508100718466_1805.png)