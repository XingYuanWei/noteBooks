# 2 Linked List Traversal


# Traversal

> 在创建了简单Linked List的之后，想要遍历Linked List节点中的每一个data，可以写一个printList()方法来用于打印Linked List  
> 中的所有元素。




```c++
    //这个方法从开始打印给定的Linked List中节点的data
    void printList(struct Node *n) 
    { 
      while (n != NULL) 
      { 
         printf("%d->", n->data); 
         n = n->next; 
      } 
    }  

```


# 完整代码
```c++
        // 一个简单程序用于测试打印出Linked List的内容
        #include<stdio.h> 
        #include<stdlib.h> 
          
        struct Node  
        { 
          int data; 
          struct Node *next; 
        }; 
          
       
        void printList(struct Node *n) 
        { 
          while (n != NULL) 
          { 
             printf(" %d ", n->data); 
             n = n->next; 
          } 
        } 
          
        int main() 
        { 
          struct Node* head = NULL; 
          struct Node* second = NULL; 
          struct Node* third = NULL; 
            
          // allocate 3 nodes in the heap   
          head  = (struct Node*)malloc(sizeof(struct Node));  
          second = (struct Node*)malloc(sizeof(struct Node)); 
          third  = (struct Node*)malloc(sizeof(struct Node)); 
           
          head->data = 1; //给第一个节点data赋值
          head->next = second; // 第一个节点的next指针指向second节点
           
          second->data = 2; //给第二个节点的data赋值 
          second->next = third;   
           
          third->data = 3;  
          third->next = NULL; 
            
          printList(head); 
           
          return 0; 
        }
```
