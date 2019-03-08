# Hashing Separate Chaining


## What is Collision
>因为Hash Function从一个很大的整数或复杂字符串键返回一个小值，所以两个键之间有可能
>产生相同的值。这种新插入的键印射出一个值，这样的值已经存在Hash Table的插槽中称作为
>碰撞。我们必须要使用一定的技巧解决这样的碰撞。

## What are the chances of collision with large table
>在一个大表中碰撞是经常发生的，一个非常简单的例子就是：即使只有23个人
>那么他们每两个人之间的是在同一天生日的概率达到了50%。


## How to handle Collision
>主要有两个方法处理碰撞  
>1.Separate Chaining  
>2.Open Addressing  


## Separate Chaining (单独链接)
>主要的思路是使得那些通过hash function返回相同值的记录在hash table的插槽中指向一个
>Linked List。  
>我们可以考虑一个简单的hash function ,"key mod 7",即把键值对7取余。 加入有键的序列为
>50，700，76，85，92，73,101

![碰撞发生](_v_images/20190308221616215_29303.png)

## Advantages
>1.实现简单  
>2.只要hash table没有被全部填上，我们可以一直添加更多的元素到链表中  
>3.对哈希函数或加载因子不太敏感  
>4.常常被用于当未知多数量和频率的键被插入和删除的时候


## Disadvantages
>1.缓存的性能不好，因为使用使用了Linked List存储。对于存在同一张表的记录，开放寻址
>对于缓存性能能够提高更好的性能。  
>2.浪费空间，因为hash table有些空间没有被使用  
>3.如果Linked List变得很长，那么搜索最糟糕的时间复杂度为O(n)  
>4.需要额外的空间存储链表指针

## Performance of Chaining
>如果每个键插入hash table插槽的可能性是相同的，那么Hahing的性能可以被估计。  
>  m = Number of slots in hash table
>  n = Number of keys to be inserted in hash table
>  
>  Load factor α = n/m 
>   
>  Expected time to search = O(1 + α)
>  
>  Expected time to insert/delete = O(1 + α)
> 
>  Time complexity of search insert and delete is 
>  O(1) if  α is O(1)


