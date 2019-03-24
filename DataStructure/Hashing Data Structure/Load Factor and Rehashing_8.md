# Load Factor and Rehashing


## Hasing如何工作
>对于插入key-value(键值对)大概需要以下几个步骤。  
>1. 将K通过hash方法转换为一个更小的数(称为哈希编码)。
>2. 哈希编码常用于查找索引，并且会首先在整个链表中查找是否已经存在K。
>3. 如果找到，则将值更新，如果没有找到，则将键值对存储在新的节点上。

## 复杂度和加载因子
>第一步，时间取决于K和哈希函数，例如，如果一个key是一个字符串"abcd"，它的hash function可能取决于字符串的长度。
>但是对于一个很大的值n，它进入map中的数量，相比于n可以几乎忽略不计，所以hash function的时间复杂度可以认为是一个
>常量O(1)。  
>对于第二步，使用index遍历整个key-value对的列表，此时有种最坏的情况就是所有的输入项n他们都有相同索引，所以时间
>复杂度为O(n)，但是如果使得哈希方法的分配每个桶的几率是平均的，那么这样一直重复的情况就不会发生。
>所以平均的情况下，如果已有n个项目添加到数组中，并且数组的长度为b，那么对于每个项目出现索引值相同 的概率为n/b，把n/b的值称为**载入因子**，
>它代表着我们map上负载。
>**载入因子**通常都要保持比较低，这样的话能够使得每个索引的出现概率减少，并且使其时间复杂度为常数O(1)。



## 再哈希(Rahashing)
>正如其名字一样，再哈希就是再一次使用哈希方法。当负载系数增加到超过其预定值（负载系数一般默认为0.75）时，
>时间复杂度增加。所以为了解决这个问题，增加数组的长度(翻倍)并且所有的值都再一次调用哈希方法，然后再存入
>新的数组中，保持其低载入因子和低时间复杂度。


## 为什么要再哈希
>在键值对插入到map中，载入因子值增大，那么意味着时间复杂度也增加了，可能不能够有较稳定的O(1)的时间复杂度。
>因此，必须要再哈希，增加数组的长度，即增加哈希桶的数量，这样以来能够有效的减小载入因子和时间复杂度。


## 如何完成再哈希
>1. 每当一个新条目进入到map中，检查载入因子
>2. 如果载入因子大于预设的值，则再哈希
>3. 对于再哈希，使得新的桶数组的大小是之前桶数组大小的两倍，并且构造新的哈希桶数组
>4. 遍历原有桶数组中的每一个元素，并且调用insert()方法插入到新的更大的桶数组中。


## Java代码实现再哈希
```java
    package Demo;

    import java.util.ArrayList;

    public class Map<K, V> {
        class MapNode<K, V> {
            K key;
            V value;
            MapNode<K, V> nextMapNode;

            public MapNode(K key, V value) {
                this.key = key;
                this.value = value;
                this.nextMapNode = null;
            }
        }

        //桶数组，存储包括键值对的节点
        private ArrayList<MapNode<K, V>> buckets;
        //已存入键值对的数量---n
        private int size;
        //数组桶的数量----b
        private int numBuckets;
        //默认的载入因子
        final double DEFAULT_LOAD_FACTOR = 0.75;

        public Map() {
            this.numBuckets = 5;
            this.buckets = new ArrayList<>(numBuckets);
            for (int i = 0; i < numBuckets; i++) {
                //初始化都为空
                this.buckets.add(null);
            }
            System.out.println("HashMap created");
            System.out.println("Number of pairs in the Map: " + size);
            System.out.println("Size of Map: " + numBuckets);
            System.out.println("Default Load Factor : " + DEFAULT_LOAD_FACTOR + "\n");
        }

        public void printMap() {
            ArrayList<MapNode<K, V>> temp = buckets;
            System.out.println("Current HashMap:");

            for (int i = 0; i < temp.size(); i++) {
                MapNode<K, V> node = temp.get(i);
                while (node != null) {
                    System.out.println("key = " + node.key + ", val = " + node.value);
                    node = node.nextMapNode;
                }
            }
            System.out.println();
        }

        public int getBucketId(K key) {
            //内置的方法
            int hashCode = key.hashCode();
            //数组的index = hashCode % numBuckets
            return hashCode % numBuckets;
        }

        public void insert(K key, V value) {
            //获得插入位置的index
            int bucketID = getBucketId(key);
            MapNode<K, V> head = buckets.get(bucketID);
            //首先循环遍历index处的所有节点并且检查key是否已经存在
            while (head != null) {
                //如果已经存在则更新该值
                if (head.key.equals(key)) {
                    head.value = value;
                    return;
                }
                head = head.nextMapNode;
            }
            // K,V组成的新节点
            MapNode<K, V> newElementNode = new MapNode<K, V>(key, value);

            head = buckets.get(bucketID);
            //把新节点插入头，把原本的头结点作为新节点的next
            newElementNode.nextMapNode = head;
            buckets.set(bucketID, newElementNode);
            System.out.println("Pair(" + key + "," + value + ")inserted successfully");
            //已添加进map中元素的个数增加
            size++;
            //计算载入因子
            double loadFactor = (1.0 * size) / numBuckets;
            System.out.println("The Load_Factor is：" + loadFactor);
            if (loadFactor > DEFAULT_LOAD_FACTOR) {
                System.out.println(loadFactor + " is greater than " + DEFAULT_LOAD_FACTOR);
                System.out.println("Therefore Rehashing will be done.\n");
                rehash();
                System.out.println("New Size of Map: " + numBuckets + "\n");
            }
            System.out.println("Number of pairs in the Map: " + size);
            System.out.println("Size of Map: " + numBuckets + "\n");

        }

        private void rehash() {
            System.out.println("\n***Rehashing Started***\n");
            ArrayList<MapNode<K, V>> temp = buckets;
            //新的桶数组是之前的两倍
            buckets = new ArrayList<MapNode<K, V>>(2 * numBuckets);
            for (int i = 0; i < 2 * numBuckets; i++) {
                //初始化为null
                buckets.add(null);
            }
            size = 0;
            numBuckets *= 2;
            for (int i = 0; i < temp.size(); i++) {
                MapNode<K, V> head = temp.get(i);
                while (head != null) {
                    K key = head.key;
                    V val = head.value;
                    //调用insert方法插入每个节点
                    insert(key, val);
                    head = head.nextMapNode;
                }
            }
            System.out.println("\n***Rehashing Ended***\n");
        }

        public static void main(String[] args) {

            // Creating the Map
            Map<Integer, String> map = new Map<Integer, String>();

            // Inserting elements
            map.insert(1, "Geeks");
            map.printMap();
            map.insert(2, "forGeeks");
            map.printMap();

            map.insert(3, "A");
            map.printMap();

            map.insert(4, "Computer");
            map.printMap();

            map.insert(5, "Portal");
            map.printMap();
        }


    }

```


## 运行结果
###### HashMap created
###### Number of pairs in the Map: 0
###### Size of Map: 5
###### Default Load Factor : 0.75
###### 
###### Pair(1,Geeks)inserted successfully
###### The Load_Factor is：0.2
###### Number of pairs in the Map: 1
###### Size of Map: 5
###### 
###### Current HashMap:
###### key = 1, val = Geeks
###### 
###### Pair(2,forGeeks)inserted successfully
###### The Load_Factor is：0.4
###### Number of pairs in the Map: 2
###### Size of Map: 5
###### 
###### Current HashMap:
###### key = 1, val = Geeks
###### key = 2, val = forGeeks
###### 
###### Pair(3,A)inserted successfully
###### The Load_Factor is：0.6
###### Number of pairs in the Map: 3
###### Size of Map: 5
###### 
###### Current HashMap:
###### key = 1, val = Geeks
###### key = 2, val = forGeeks
###### key = 3, val = A
###### 
###### Pair(4,Computer)inserted successfully
###### The Load_Factor is：0.8
###### 0.8 is greater than 0.75
###### Therefore Rehashing will be done.
###### 
###### 
###### ***Rehashing Started***
###### 
###### Pair(1,Geeks)inserted successfully
###### The Load_Factor is：0.1
###### Number of pairs in the Map: 1
###### Size of Map: 10
###### 
###### Pair(2,forGeeks)inserted successfully
###### The Load_Factor is：0.2
###### Number of pairs in the Map: 2
###### Size of Map: 10
###### 
###### Pair(3,A)inserted successfully
###### The Load_Factor is：0.3
###### Number of pairs in the Map: 3
###### Size of Map: 10
###### 
###### Pair(4,Computer)inserted successfully
###### The Load_Factor is：0.4
###### Number of pairs in the Map: 4
###### Size of Map: 10
###### 
###### 
###### ***Rehashing Ended***
###### 
###### New Size of Map: 10
###### 
###### Number of pairs in the Map: 4
###### Size of Map: 10
###### 
###### Current HashMap:
###### key = 1, val = Geeks
###### key = 2, val = forGeeks
###### key = 3, val = A
###### key = 4, val = Computer
###### 
###### Pair(5,Portal)inserted successfully
###### The Load_Factor is：0.5
###### Number of pairs in the Map: 5
###### Size of Map: 10
###### 
###### Current HashMap:
###### key = 1, val = Geeks
###### key = 2, val = forGeeks
###### key = 3, val = A
###### key = 4, val = Computer
###### key = 5, val = Portal