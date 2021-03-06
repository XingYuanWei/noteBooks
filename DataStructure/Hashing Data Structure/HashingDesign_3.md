# Hashing Design


## Abstract
> 假定我们想要设计一个系统用于存储雇员信息，用他们的电话号码作为键。并且我们希望能够执行以下的有效查询。  
> 1. 插入一个电话号码和相应的信息
> 2. 搜索到电话号码和获取信息
> 3. 删除一个电话号码和相关的信息

> 我们可以想到使用以下的数据结构保存关于不同电话号码的信息  
> 1. 电话号码和记录的数组
> 2. 电话号码和记录的Linked List
> 3. 用电话号码作为键的二叉搜索树
> 4. 直接访问表


## 分析
>#### 1.
>对于数组和链表，通常需要线性的时间用于搜索，这样的方式在实际情况中花费是十分昂贵的。
>#### 2.
>如果我们使用数组并且保证其数据的排序，使用二叉搜索树查询电话号码， 这样花费的时间复杂度为
>O(logn),但是插入和删除操作消耗不小并且还需要额外的保存排序状态。
>#### 3.
> 对于平衡二叉树，我们可以使用比较折中(中等，温和)的方式，对于插入和删除，所有的
> 这些操作都能保证时间复杂度为O(Logn)。
>#### 4.
> 另一种解决方案是我们可以制造一个大数组并在数组中使用电话号码作为索引，
> 制造一个比较大的直接访问表。输入一个电话号码，如果该电话号码存在，
> 则返回对应的记录。这个方法比以上所有的方法都要好，因为我们可以
> 确保时间复杂度都为O(1)。例如我们要插入一个电话号码信息，我们可以使用给定的电话号码
> 信息和它的细节创建一条记录，使用电话号码作为索引并且存储让指针指向这个被创建的记录。
> 但是这个方法有着许多的实际限制，首先的问题就是所需要的额外空间是巨大的，将电话号码作为数组的
> 索引，如果一个电话号码有n个数字，则需要的空间为O(m*10^n)，m为记录数。
> 另一个问题就是编程语言中不会存储n个数字组成的整数。


> 由于直接访问表以上种种的限制，从而使得它常常不能被使用。Hashing是解决上述问题
> 的一个好方法，并且Hashing就像数组一样比以上Linked List，平衡二叉搜索树这些数据结构在实际中
> 表现的都更好。对于Hashing如果合理的情况下平均时间复杂度为O(1)，然而最坏的情况下时间复杂度
> 为O(n)。  
> Hashing是对直接访问表的一种改善，主要思路是将一个给定的电话号码或其他键转换为更小的数字，
> 使用更小的数字作为一个表的索引，这样的表称为hash table。


## Hash Function
>将一个给定的电话号码转换成一个实际很小的整数值，这个印射出的整数值常常被用于hash table的索引，
>简单的情况下，一个hash将一个很大的数或复杂的字符串印射为一个很小的整数，使得这个数能够被用于
>hash table的索引。一个好的hash function有如下的性质：
>1. 计算十分的效率  
>2. 平均分配键  
>例如，对于电话号码，错误的分配方法是取前三位数字，更好的方法是取最后的三位数，当然了，这也不是
>最后的hash function，还有比这更好的方式。

## Hash Table
> 一个存着指向与给定电话号码对应的记录的指针数组。一个对于给定hash table的输入，
> 如果没有电话号码的hash function值等于条目的索引，则hash table中条目为NULL
> 提示：  
> 1. nil是一个对象值，如果要把一个对象设置为空的时候就用nil。
> 2. Nil是一个类对象的值，如果要把一个Class类型的对象设置为空的时候就用Nil。
> 3. NULL是一个通用指针。
## Collision Handing
>因为对于一个很大的键，hash function会返回一个很小的值，所以有可能两个键会返回一个相同的结果。
>新插入的一个键印射到hash table中已有的插槽，这样情况称作为碰撞，并且发生这种情况必须采用一些
>碰撞处理技巧。以下为碰撞处理原则。  
>1. Chaining：主要思路是使得那些通过hash function返回具有相同值的记录在hash table中用Linked List存储。
>这个方式是十分简单的，但是需要额外的存储空间。
>2. Open Addressing：在开放寻址中，所有元素都存储在hash table本身，每个表条目包含记录或为空，
>在搜索元素时，我们逐个检查表槽，直到找到所需的元素，或者确定元素不在表中。