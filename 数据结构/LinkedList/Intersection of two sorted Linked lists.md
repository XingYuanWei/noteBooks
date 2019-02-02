# Intersection of two sorted Linked lists



>给定两个已排序的逐渐递增的数组，求两个Linked List的交集，并返回一个新的list，旧有的两个list不应被改变。
>例如，第一个list为1->2->3->4->6，第二个list为2->4->6->8。则返回的新list应为2->4->6。

## 方法一
>以下方法为用c++的STL完成的。代码如下

```c++
    Node * returnIntersectionList(Node * listOne, Node * listTwo)
    {
    	set<int> set;
    	vector<int> interVector;
    	struct Node* head_first = listOne;
    	struct Node* head_second = listTwo;
    	while (head_first != NULL && head_second != NULL)
    	{
    		set.insert(head_first->data);
    		head_first = head_first->next;
    	}
    	while (head_second != NULL) {
    		if (set.count(head_second->data))
    		{
    			interVector.push_back(head_second->data);
    		}
    		head_second = head_second->next;
    	}
    	if (!interVector.empty())
    	{
    		struct Node* returnHead = NULL;
    		struct Node* preNode = NULL;
    		for (vector<int>::iterator it = interVector.begin(); it < interVector.end(); it++) {
    			//分配新节点的内存
    			struct Node* currNode = (struct Node*)malloc(sizeof(struct Node));
    			currNode->data = *it;
    			if (returnHead == NULL)
    			{
    				returnHead = currNode;
    			}
    			else
    			{
    				preNode->next = currNode;
    			}
    			preNode = currNode;
    		}
    		return returnHead;
    	}
    	cout << "No Intersection";
    	return nullptr;
    }
```
## 思路
>使用c++的STL库的方法十分简单，只要使用set即可。set在STL库中用于存储集合中唯一的元素，所以上面的代码首先把链表一的所有元素先添加进set中，
>然后遍历链表二，通过count()方法判断链表二中是否存在于链表一中相同的元素，如果存在则把其添加进一个vector容器中。之后遍历该vector容器，vector
>容器装的是节点值，创建具有这些值的节点，连接成新的链表。返回该链表的头结点。

## 方法二：





