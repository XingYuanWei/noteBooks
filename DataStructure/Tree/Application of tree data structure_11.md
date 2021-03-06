# 树的应用


## Abstract
> 不像数组和链表是线性数据结构，树是分层(或非线性)数据结构。


## 应用
>1. 使用树的一个原因可能是因为您希望存储自然形成层次结构的信息。例如，计算机上的文件系统： 文件系统

              /   <-- root
          /      \
        ...        home
              /          \
           ugrad        course
            /          /    |    \
          ...        cs101 cs112 cs113


>2. 如果我们以树的形式组织键(有一些顺序，如BST)，我们可以在适当的时间内搜索给定的键比链表快，比数组慢。
>像AVL和红黑树这样的自平衡搜索树保证了搜索的O(Logn)上界。
>3. 我们可以在适度的时间内插入/删除键（比数组快，比无序链接列表慢)
>自平衡搜索树（如AVL和红黑树）保证插入/删除O（Logn）的上限。
>4.与链表和数组不同，树的指针实现对节点数量没有上限，因为节点是使用指针链接的。

## 其他应用
> 1.堆是使用数组实现的树状数据结构，用于实现优先级队列。
> 2.B树和B+树：它们用于在数据库中实现索引。
> 3.语法树:用于编译器。
> 4.K-D树：用于组织K维空间中的点的空间分区树
> 5.Trie：用于实现带前缀查找的字典。
> 6.后缀树：用于在固定文本中快速搜索模式。