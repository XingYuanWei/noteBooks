# Introduction


## Abstract

> A Double Linked List(DLL)包含了一个额外的指针，通常称为previous指针，和next指针和数据域data一并的存在于单链表Linked List中。
> 如下图所示：

> ![DLL的结构示意图](_v_images/20190202231249984_9043.png)

>用c语言代码来表示一个双链表的节点的如下

```c++
    struct Node{
        int data;
        struct Node* next;
        struct Node* prev;
    }
```
## 以下是Doubly Linked List和Singly Linked List相比的优点和缺点

### 与Singly Linked List相比的优点
>1. Doubly Linked List能够直接的向前遍历和向后遍历
>2. 如果事先给定了要被删除节点的指针则DLL的删除操作将会更有效
>3. 我们能够在给定的一个链表中快速的插入一个新节点，在一个单链表中，如果删除一个节点，则需要一个指向前面的指针。为了
>得到这样一个指向前节点的指针，我们往往需要通过遍历的方式。在DLL中，我们只需要使用previous指针就能获得指向前一个节点的指针。


### 与Singly Linked List相比的劣势
>1. 每个节点需要额外的空间存放的previous指针(可以用单链表实现Doubly Linked List，后面章节介绍)
>2. 所有的操作都需要的维护一个额外的指针。例如在插入操作的时候，我们需要和next指针一样也要去更改previous指针。
>这样就使得需要额外的几个步骤用于操作previous指针。


## 插入操作
>一个节点能够有四种方式插入到DLL中
>1. 插入在DLL的最前面
>2. 插入在给定节点的后面
>3. 插入在DLL的最后面
>4. 插入在给定节点之前

## 插入在DLL的最前面
> 完成插入到DLL最前面需要五个步骤
> 我们如果给定了节点为10->15->25->20，如果我们要添加一个节点5在前端，那么此时链表将成为5->10->15->25->20。
> 和Singly Linked  List类似，也把DLL插入节点到最前端的方法称为push，该push方法同样的也接收一个参数，该参数为DLL
> 的指向头结点的指针，因为push方法一定要改变头的节点使其指向新的节点。如下图所示：
> 
> ![插入节点在DLL的最前方](_v_images/20190202231158588_15058.png)
