# Open Addressing
> 像使用分离链表一样，开放寻址也是一个处理碰撞的方法。在开放寻址中，所有的元素都能存储在
> hash table中，所有在任何时候，表的大小一定要大于或等于键的总数。
>insert(k)：持续搜索直到发现新的空插槽，一旦发现一个新的空插槽，则插入k  
>search(k)：持续搜索直到槽的键不等于k或到达一个空槽为止  
>delete(k)：删除操作十分有意思，如果我们冒然的删除一个键，那么可能会导致之后的search方法
>失败，所以槽中的键只是被标记为"deleted"而不是真的删除了，插入时候则可以把这个被标记"deleted"
>的元素覆盖。但是搜索的时候不会在这个被标记元素中停止。




## 开放寻址按以下方式完成
#### 1.线性探测
>例如：我们使用哈希方法hash(x)计算出槽的索引，S表示表的大小  
>如果hash(x) % S计算出的槽是有数值的，那么我们尝试(hash(x)  + 1) % S  
>如果(hash(x) + 1) % S也是满的，那么我们尝试(hash(x) + 2) % S  
>如果(hash(x) + 2) % S也是满的，那么我们尝试(hash(x) + 4) % S
>..................  
>让我们想象一个简单的hash  function比如 "key mod 7"，并且有序列50,700，76，85,92，73，101

![线性探测](_v_images/20190312080904564_28728.png)
>线性探索的问题是聚集，当有许多连续的元素形成了一个组，那么我们可能将花费很大的时间用于搜索元素和发现空的桶。

#### 2.平方搜索
>例如：我们使用哈希方法hash(x)计算出槽的索引，S表示表的大小    
>如果hash(x) % S计算出的桶是满的，则我们尝试(hash(x) + 1 * 1) % S  
>如果(hash(x) + 1 * 1) % S也是满的，则我们尝试(hash(x) + 2 * 2) % S  
>如果(hash(x) + 2 * 2) % S也是满的，那么我们尝试(hash(x) + 3 * 3) % S  
>..........

#### 3.双哈希法
>我们使用另一个hash function名为hash2(x)，并且查找i * hash2(x)。
>如果hash(x) % S是满的，那么则尝试(hash(x) + 1 * hash2(x)) % S  
>如果(hash(x) + 1 * hash2(x)) % S是满的，则我们尝试(hash(x) + 2 * hash2(x)) % S  
>如果(hash(x) + 2 * hash2(x)) % S是满的，则我们尝试(hash(x) + 3 * hash2(x)) % S  
>..........


## 三种方法的比较
>线性探测有着最好的缓存性能但是可能会发生元素聚集问题，另一个优点就是线性探测易于计算。  
>平方探测法在缓存性能与聚集方面介于两者之间。  
>双哈希法的缓存性能很差但是没有聚集问题，双哈希法需要更多的计算时间并且需要两次计算。

## 链表法与开放寻址法比较

| S.No. |                                          **Seperate Chaining**                                          |                                     **Open Addressing**                                     |
| ----- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 1.    | Chaining is Simpler to implement.                                                                       | Open Addressing requires more computation.                                                   |
| 2.    | In chaining, Hash table never fills up, we can always add more elements to chain.                       | In open addressing, table may become full.                                                   |
| 3.    | Chaining is Less sensitive to the hash function or load factors.                                        | Open addressing requires extra care for to avoid clustering and load factor.                 |
| 4.    | Chaining is mostly used when it is unknown how many and how frequently keys may be inserted or deleted. | Open addressing is used when the frequency and number of keys is known.                      |
| 5.    | Cache performance of chaining is not good as keys are stored using linked list.                         | Open addressing provides better cache performance as everything is stored in the same table. |
| 6.    | Wastage of Space (Some Parts of hash table in chaining are never used).                                 | In Open addressing, a slot can be used even if an input doesn’t map to it.                   |
| 7.    | Chaining uses extra space for links.                                                                    | No links in Open addressing                                                                  |



## 开放寻址的性能
>像链表法一样可以计算出hashing的性能在所有的键插入表中的每个槽都有相同的概率下。  
>m = 表中桶的个数  
>
>n = 要在hash表中插入键的个数  
>
>载入因子 load factor α = n / m (<1)  
>
>预期的插入/搜索/删除的时间为1/(1-α)  
>
