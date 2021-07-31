# CPT201 database

## W2: index and B+ tree

* learning outcome：
  *  The structure of the index
  * Order index
  * Primary index vs. Secondary index
  * Dense Index vs. Spare Index
  * Multilevel index

### the Structure of Index

https://www.guru99.com/indexing-in-database.html

**Data file**: collection of blocks holding records of on disk. 就是在硬盘中存储数据的集合

**Index file:** 一种数据结构允许DBMS高效的在**Data file**中找到你想要的值

* Index file 由以下数据组成（也被叫做<mark>index entries</mark>)

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210715143054446.png" alt="image-20210715143054446" style="zoom:50%;" />

**Search key**: 在file中一组用来查找记录的属性

**search key和pointer的关系：** 

### order index:  index entries are sorted on the search key value.

#### order index can be **Dense index** or **sparse Index**

* Dense index:意思就是在Data file中所有search key都有一个index entry<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210715161407393.png" alt="image-20210715161407393" style="zoom:50%;" />

<mark>Search key 可以不是primary key!!! 你看上面这图，它的search key就是部门！！！</mark>

如果索引文件中不存在，那么就表示主文件中一定也不存在

Candidate key： 主文件可以不是order的

non-candidate key：如果索引文件的索引字段不是重复的那么主文件就必须得是order的<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210724205052910.png" alt="image-20210724205052910" style="zoom:50%;" />

如果索引文件的字段可以重复那么主文件可以不是order的

或者引入桶也就是辅助索引

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210724205154653.png" alt="image-20210724205154653" style="zoom:50%;" />



* Spares index：意思就是在Data file中不是所有的search key都有index entry**必须是排好序的**<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210715161219115.png" alt="image-20210715161219115" style="zoom:50%;" />

搜索文件中不存在的值不一定代表主文件中没有，就比如Downtown，但如果你想检索它的话

* 首先找到相邻的小于D的的最大索引字段所对应的索引项
* 从该索引项从该索引项所对应的记录开始顺序检查，如果存在的话找到就行，如果不存在，找到比Downtown大的位置
* 比起dense index的优势：空间占用更少，维护任务更轻，但速度更慢

#### order idnex can also be Primary index or Secondary index

* Primary index(clusting index): 主索引是稀疏索引

通常是对每一个储存块有一个索引项，索引项的总数和存储表所占有的存储块数目相同，存储表的每一个存储块块的第一条记录。

* Secondeary index(non-clustering、稠密索引):

辅助索引：

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210724211204319.png" alt="image-20210724211204319" style="zoom:30%;" />

#### 主索引vs辅助索引

一个主文件仅可以仅有一个主索引，但可以有多个辅助索引，主索引通常建立在主码上面，辅助索引建立在其他属性上面

#### 聚簇索引和非聚簇索引

* 聚簇索引是指索引中临近记录在主文件也是临近存储的
* 非聚簇索引是指索引中邻近存储的在主文件中不一定是邻近存储的

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210724222219422.png" alt="image-20210724222219422" style="zoom:50%;" />







### B+ tree index

* <mark>n</mark> is the number of pointers in a node.
* root must have at least two **children.**
* In each non-leaf node(other than the root) has between **⌈n / 2⌉** and n children
* the root has between 2 and n children.
* Each leaf node must contain at least⌈(n-1) / 2⌉ keys.
* height is no more than ⌈log<sub>⌈n/2⌉</sub>(K)⌉

#### B+树查询

>**function** find(v)
>/**
>	Assume no duplicate keys, and returns pointer to the record with search key value v if such a record exists, and null otherwise
>	*/
>  Set C = root node
>  **while**(C is not a leaf node) **begin**
>    Let i = smallest number such that  v <= C.K<sub>i</sub>
>
>​    if there is no such number i **then begin**
>
>  		Let P<sub>m</sub> = last non-null pointer in the node
>
>​		  Set C = C.P<sub>m</sub>
>
>​		  **end**

#### Update on B+ Trees

如果一个节点的poniter个数小于**⌈n / 2⌉**或者过多那么这个节点就得合并或是分裂。

##### insertion：

刚插入进去的时候先观察leaf-node是否满，如果满了话就得分裂，一般是前**⌈n / 2⌉**在原来的节点，剩下的在新生成的节点,然后呢父节点还要一个新的search-key和pointer去指向新的node，如果父节点还有位置直接建就完事了，然后再整一个新的pointer去指向新的节点。

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210716153159983.png" alt="image-20210716153159983" style="zoom:50%;" />

如上图，如果你想插入"Adams",首先你得找到要插入的位置，也就是叶节点中最左边的节点，发现满了，所以呢就得分裂，运用公式**⌈n / 2⌉**可得前两个在新节点，剩下俩在新节点，然后呢得去在父节点建立一个新的search-key和node去指向刚才创建的叶节点，最终结果如下图

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210716153657726.png" alt="image-20210716153657726" style="zoom:50%;" />



Non-leaf节点的分裂跟leaf节点分裂不太一样：

先把这个满的节点再加上从子节点提上来的节点合并一下，然后用公式计算出要分裂的点，也就是**⌈(2/n⌉**,然后再把这个节点继续往上套，跟递归一样

non-leaf节点分裂跟leaf节点分裂有点不一样：就比如接着用上面这个图片来举例说明，此时你想插入"Lamport"，先找到。。。结果如下图

![image-20210716175258720](/Users/shinbouei/Library/Application Support/typora-user-images/image-20210716175258720.png) 

##### Deletion:

先看能不能**merge sibling**如果sibling也太少的话就需要**redistribute pointers:**

因为merge完之后呢原来空node的父节点的指针和search key也得删掉，这种情况可能会导致父节点也变的太空所以就得考虑合并或是重新分配

## Week 3 Hash Index：

* 静态哈希
* 动态哈希

会了～

## Week4a Relational Algebra:

* Six basic operation
  * select: σ
  * project: ∏
  * union: ∪
  * set difference: -
  * Cartesian product: x
  * rename: ρ
* Additional Operations 
  * Set intersection
  * Natural join
  * Division
  * Assignment

### Select Operation 

Relation R:<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718155019758.png" alt="image-20210718155019758" style="zoom:50%;" />

σ<sub>A=B ^ D > 5</sub> (r)<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718155041316.png" alt="image-20210718155041316" style="zoom:50%;" />

Notation: σ <sub>p</sub>(r)

p也被叫做：**selection predicate**

### Project Operation

Relation r：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718160036332.png" alt="image-20210718160036332" style="zoom:50%;" />

∏<sub>A,C</sub> (*r*):<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718160111985.png" alt="image-20210718160111985" style="zoom:50%;" />

记得要删除相同项哦

### Union Operation

Notation: r ∪ s

### Set Difference Operation –

Relations r, s	<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164058686.png" alt="image-20210718164058686" style="zoom:50%;" />

r–s<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164119813.png" alt="image-20210718164119813" style="zoom:50%;" />

r-s就是在r中减去s中的

### Cartesian-Product Operation

Relations r, s：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164257985.png" alt="image-20210718164257985" style="zoom:50%;" />

rxs<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164321534.png" alt="image-20210718164321534" style="zoom:50%;" />

### Set-Intersection Operation

Relation r, s：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164755218.png" alt="image-20210718164755218" style="zoom:50%;" />

r ∩ s ：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718164810222.png" alt="image-20210718164810222" style="zoom:50%;" />

### Natural Join Operation 

Relation r, s:<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718165611917.png" alt="image-20210718165611917" style="zoom:50%;" />

r⋈s<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718165639315.png" alt="image-20210718165639315" style="zoom:50%;" />

自然链接就是比如现在有两个关系a和b，a⋈b就是吧a和b相同的属性先找出来，然后吧相同的进行连接，不一样的删除

### Division Operation

Relations r, s    <img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718170455562.png" alt="image-20210718170455562" style="zoom:50%;" />



r ÷ s:<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718170511001.png" alt="image-20210718170511001" style="zoom:50%;" />

Example2:

Relations r, s：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718175354719.png" alt="image-20210718175354719" style="zoom:50%;" />

r÷s：<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210718175409685.png" alt="image-20210718175409685" style="zoom:50%;" />

第一步：先在r中删除不包含s属性的列

第二步：s中的每一列跟在r中都能找到

第三步：删除重复

## Week4b **Query Evaluation - Selction**:

* Basic steps in query processing
* How to measure query costs
* Algorithms for evaluating realtional algebra operations(Selection and Projection)
* External Merge sort



### Measures of Query Cost

* <mark>t<sub>T</sub></mark> – time to transfer one block

* <mark>t<sub>S</sub></mark> – time for one seek
* Cost for b block transfers plus s seek:<mark>b * t<sub>T</sub> + s * t<sub>S</sub></mark>

我们在表达是中不包含写入磁盘所花费的时间

### Evaluation of Selection Operation

#### **File scan** – search algorithms that scan files and retrieve records that fulfill a selection condition.

也就是一个一个扫描

* liner scan: cost : 1 seek B<sub>r</sub> transfer
  * r如果发现一个key attribute 就停止的话：Average cost = (b<sub>r</sub> /2) block transfers + 1 seek
* Binary scan : seek 和 transfer 都是⎡log<sub>2</sub>b<sub>r</sub>⎤* (t<sub>T</sub> + t<sub>S</sub>) 

#### **Index scan** – search algorithms that use an index

 selection condition must be on search-key of index.

##### primary index 

candidate key：transfer和 seek都是一样的

* 例如B+tree :(h<sub>i</sub> +1)* (t<sub>T</sub> + t<sub>S</sub>)  ps.hi是树的高度且发现的是单一节点

Non-candidate key: h<sub>i</sub> *(t<sub>T</sub> +t<sub>S</sub>)+t<sub>S</sub> +t<sub>T</sub> *b ps.  Let b = number of blocks containing matching records

##### secondary index

一条记录：(h<sub>i</sub> +1)* (t<sub>T</sub> + t<sub>S</sub>)   

多条记录(h<sub>i</sub> +n)* (t<sub>T</sub> + t<sub>S</sub>)  

 ### 排序

  relation是否能放进内存：

* 能：1次扫描搜索+ b<sub>r</sub>块传输

* 不能：external sort merge:

  * Let *M* denote the number of blocks in the main memory buffer available for sorting, that is, the number of disk blocks whose contents can be buffered in available main memory.

    transfer: b<sub>r</sub>(2⌈log<sub>⌊*M*∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ + 1) 

    Seek:2⌈b<sub>r</sub>∕M⌉ + ⌈b<sub>r</sub>∕b<sub>b</sub>⌉(2⌈log<sub>⌊M∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ − 1)

#### Algorithm for Selection Operation (File scan: *l inear search*)

* Scan each file block and test all records to see whether they satisfy the selection condition.

  * <mark>Cost estimate = b<sub>r</sub> block transfers + 1 seek</mark>

    * br denotes number of blocks containing records from

      relation r

  * If selection is on a key attribute, can stop on finding record (Linear Search, Equality on Key)

    * <mark>Average cost = (br /2) block transfers + 1 seek</mark>

#### Algorithms for Selection Operation (File scan: *binary search*)

* Applicable only if the selection is an equality comparison on the attribute on which file is <mark>**ordered.**</mark>
  * 花费估计(block transfer和seek的数)：
    * 发现所要查找的第一个tuple在block当中⎡log2(b<sub>r</sub>) *  (t<sub>T</sub> + t<sub>S</sub>)⎤
      * 如果有多个符合的record,添加transfer成本
      * 将会在之后进行讨论

#### Selections Using Indices (*primary index on candidate key, equality*).

* Retrieve a single record that satisfies the corresponding equality condition
  * **Cost=(h<sub>i</sub> +1)*(t<sub>T</sub> +t<sub>S</sub>) **
* 要记得b+树index的高度最高是**⎡log<sub>⎡n/2⎤</sub>(K)⎤** :其中n是节点的指针数量，k是的search key数量
  * 例如：一个关系r有1000000个不同的search key，并且每个节点有100个index entry 所以h<sub>i</sub> = 4
* Retrieve possibly <mark>multiple</mark> records （检索多个记录）：
  * Records will be on consecutive blocks
    * Let b = number of blocks containing matching records
    * **Cost=h<sub>i</sub> *(t<sub>T</sub> +t<sub>S</sub>)+t<sub>S</sub> +t<sub>T</sub> *b**
* Retrieve a **single** record if the search-key **is a candidate key**
  *   Cost=(h<sub>i</sub> +1)*(t<sub>T</sub> +t<sub>S</sub>)
* Retrieve **multiple** records if search-key is **not a candidate key**
  * each of n matching records may be on a different block
  * Cost at most is ：**(h<sub>i</sub> +n)*(t<sub>T</sub> +t<sub>S</sub>)**
  * 如果n非常大的话，花销会非常大，注意搜索时间取决于n

#### Comparative Selections σ*A*≤*V* (*r*) or σ*A* ≥ *V*(*r*)

不明白

#### Sorting

为啥需要排序呢，因为一些算法的前提是他们要排序好的

#### External Merge Sort 

* 一个关系存储了b<sub>r</sub> blocks, M 是内存的大小, so the number of run file **b<sub>r</sub> / M**

* buffer size b<sub>b</sub> (read  b<sub>b</sub> blocks at a time from each run and  b<sub>b</sub> blocks for writing)

* Cost of Block Transfer 

  * 总merge 传递花费所需要:**⎡log<sub>⌊M/b<sub>b</sub>⌋–1</sub>(b<sub>r</sub>/M)⎤**. Each time can merge **⌊(M-b<sub>b</sub>)/b<sub>b</sub>⌋.**

  * Block transfers for initial run creation as well as in each pass is 2b<sub>r</sub> (read/write all b<sub>r</sub> blocks)

    * for final pass, we don’t count write cost
    * hus total number of block transfers for external sorting:

    **<mark>2b<sub>r</sub> + 2b<sub>r</sub> ⎡log<sub>⌊M/b<sub>b</sub>⌋–1</sub>(b<sub>r</sub> / M)⎤ - b<sub>r</sub> = br ( 2 ⎡log<sub>⌊M/b<sub>b</sub>⌋–1</sub>(b<sub>r</sub> / M)⎤ + 1)</mark>**

* Cost of seeks

  * During run generation: one seek to read each run and one seek to write each run

  * 2 ⎡b<sub>r </sub>/ M⎤

  * During the merge phase

    * Need 2 ⎡br / bb⎤ seeks for each merge pass
    * Total number of seeks:

    **<mark>2 ⎡b<sub>r</sub> / M⎤ + ⎡b<sub>r</sub> / b<sub>b</sub>⎤ (2 ⎡log<sub>⌊M/b<sub>b</sub>⌋-1</sub> (b<sub>r</sub> / M)⎤ -1)</mark>**

## Week4c **Query Evaluation - Join**

* **Algorithms for evaluating join operators**
* **Algorithms for evaluating other expressions**

### Natural-Join Operation

* Nested-loop join
* Block nested-loop join
* Indexed nested-loop join
* Merge-join
* Hash-join

### Nested-Loop Join

The simplest join algorithms, that can be used independently of everything (like the linear search for selection)

<mark>r is called the **outer relation** and s the **inner relation** of the join.</mark>

这个贼重要，会影响结果

* 最坏的情况下， if there is enough memory only to hold one block of each relation,n<sub>r</sub> 是relation r的tuples数目。所以estimate的花费是：
  * <mark>n<sub>r</sub> * b<sub>s</sub> + b<sub>r</sub> block transfers, plus n<sub>r</sub> + b<sub>r</sub> seeks</mark>

* If the 任意  relation fits entirely in memory, use that as the inner relation.(最好情况)
  * <mark>Reduces cost to b<sub>r</sub> + b<sub>s</sub> block transfers and 2 seeks</mark>

* <mark>通常来说，选取选取**block较小**的关系作为**outer**的关系。</mark>
* 所以说，选择inner和outer取决于每个relation关系的szie

### Block nested-loop join

* 最坏情况：<mark>b<sub>r </sub>* b<sub>s</sub> + b<sub>r</sub> block transfers and  2 * b<sub>r</sub> seeks</mark> 
  * Each block in the inner relation s is read once for each block in the outer relation (instead of once for each tuple in the outer relation).

最好情况(when smaller relation fits into memory)：<mark>b<sub>r</sub> + b<sub>s</sub> block transfers plus 2 seeks.</mark>

### index Nested - loop Join

* For each tuple tr in the outer relation r, use the index on s to look up tuples in s that satisfy the join condition with tuple tr.

* 最坏情况； buffer has space for only one page of r, and, for each tuple in r, we perform an index lookup on s.

* Cost of the join: <mark>b<sub>r</sub> + n<sub>r</sub> * c </mark>block transfers and seeks

  * Where c is the cost of traversing index and fetching all matching s (c是查询消耗)

     tuples for one tuple in r

  * **c** can be estimated as cost of a single selection on s using the join condition (usually quite low, when compared to the join)

* <mark>一般是有索引的作为内层，如果两个关系上都有索引的话，一般把tuple较小的作为外层关系</mark>

* 连接时间代价是：<mark>b<sub>r</sub>(t<sub>T</sub> + t<sub>S</sub>) + n<sub>r</sub> * c</mark>

#### Example of Indexed Nested- Loop Join Costs

height is no more than ⌈log<sub>⌈n/2⌉</sub>(K)⌉

Compute depositor ⋈ customer, with **depositor** as the **outer** relation.

* 让customer有b+tree索引 on the join attribute customer-name, with n = 20
* indexed nested loops join的花费是：100 + 5000*（1+4） = 25100 block transfer和seek

### Merge sort join

* 只可以在等值连接和自然链接中
* merge join的花费是(B<sub>b</sub>是blocks是每个关系中分配在内存中的block数)：b<sub>r</sub> + b<sub>s</sub> block transfers +⎡b<sub>r</sub>/b<sub>b</sub>⎤+⎡b<sub>s</sub>/b<sub>b</sub>⎤ seeks
* <mark>如果这个关系没排序还得加上排序的花销，要加上两次transfer和seek</mark>
  * 比如现在俩关系都没排序，所以先算merge sort的transfer和seek，再加上两次的join的transfer和seek

#### merge sort

merge sort 和 merge sort join不一样

Let *M* denote the number of blocks in the main memory buffer available for sorting, that is, the number of disk blocks whose contents can be buffered in available main memory.

transfer: b<sub>r</sub>(2⌈log<sub>⌊*M*∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ + 1) 

Seek:2⌈b<sub>r</sub>∕M⌉ + ⌈b<sub>r</sub>∕b<sub>b</sub>⌉(2⌈log<sub>⌊M∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ − 1)



### Hash index

* 也只适用于自然链接和等值连接

* A hash function h is used to partition tuples of both relations

* The cost of hash join is

  3(b<sub>r</sub> + b<sub>s</sub>) + 4 * n<sub>h</sub> block transfers, and

  2(⎡b<sub>r</sub>/b<sub>b</sub>⎤+⎡b<sub>s</sub>/b<sub>b</sub>⎤)+2*n<sub>h</sub> seeks

  * n<sub>h</sub>是partition<mark>当题目出现了partition就说明是hashjoin</mark>的块数
  * b<sub>b</sub>是缓冲区的块数

* If the entire build input can be kept in main memory (then no partitioning is required), **Cost estimate goes down to br + bs and 2 seeks.**

  * b<sub>b</sub>：some blocks of memory(b<sub>b</sub>) are reserved as the output buffer for each partition.



## Week5a **Query** **Optimisation 1** 1.40/3

V（A,r）：关系r中属性A中出现非重复值的个数，如果A是关系r上的主码则V(A,r)等于nr

物化：中间操作需要写回磁盘

* pipeline：不需要写回
  * hash join sort不能用pipeline
  * 只有nested looped join 和排好序的Merge join 可以用

如何把图转换为表达式

### 优化策略：

#### 选择优先

### estimation size

目录信息：

* n<sub>r</sub>:关系r的tuple个数
* b<sub>r</sub>关系r的磁盘块树
* f<sub>r</sub>一个磁盘块能装r中tuple的个数
* v(A,R):r关系中A属性非重复的个数

* b<sub>r</sub> = ⌈n<sub>r</sub>/f<sub>r</sub>⌉

##### selection estimation size

1. 等值比较：σ<sub>A</sub> = V(r)
   1. 均匀分布：n<sub>r</sub> / V(A,r). ==> V(A,r) ✖️ 重复次数 = n<sub>r</sub>   ps.针对非primary key
   2. 如果是primary key 直接就是1
2. 非等值比较：寻找σ<sub>A</sub> <= V(r)  寻找V<sub>(r)</sub> < min

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-31 01.58.12.png" alt="截屏2021-07-31 01.58.12" style="zoom:30%;" />

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-31 01.59.24.png" alt="截屏2021-07-31 01.59.24" style="zoom:30%;" />



1. 

##### join R<sub>1</sub>⋈R<sub>2</sub> 

* r ∩ s = 空 （表示r 和s没有相交的属性）
* r ∩ s = 非空 且r ∩ s = 

## Week5b **Query** Optimisation 2

### 代数优化的启发式规则：

* 选择运算尽量先做：减少中间集的规模
* 投影运算和选择运算同时进行：避免重复扫描
* 将投影运算与其前后的双目运算结合起来：避免重复扫描

* 某些选择运算+其前面的笛卡尔积 ==〉连接运算（减少中间集的规模）
  * σ<sub>S.<sub>sno</sub></sub> = SC.<sub>sno</sub>(S ✖️SC)  ==〉S ⋈ SC

将sql语句转换为查询树

<img src="/Users/shinbouei/Downloads/IMG_0015.jpg" alt="IMG_0015" style="zoom:30%;" />

## **Lecture 6a:** **Transaction Management – Concepts of Transaction**

* A <mark>transaction</mark> is a unit of program execution that accesses and possibly updates various data items.
  * A transaction must see a consistent database.
  * During transaction execution the database may betemporarily inconsistent.
  * When the transaction completes successfully (is committed), the database must be consistent.
  *  After a transaction commits, the changes it has made to the database persist, even if there are system failures.

* Two main issues to deal with:
  * Concurrent execution of multiple transactions
  * Recovery from failures of various kinds, such as hardware failures and system crashes

* 原子性：Either all operations of the transaction are properly reflected in the database or none are.
* 一致性：Execution of a transaction in isolation preserves the consistency of the database.  
* 隔离型：Although multiple transactions may execute concurrently, each transaction must be unaware of other concurrently executing transactions. Intermediate transaction results must be hidden from other concurrently executed transactions.
  * 
* 持久性：After a transaction completes successfully, the changes it has made to the database persist, even if there are system failures.

### Schedule调度

执行在系统中的执行的时间顺序

Serialisability 可串行化

### Conflicting

#### conflict can be identified 

* Write-read(WR) conflict: reading uncommintted data 读到了未提交的数据
* Read-write(RW) confilct: unrepeatable read 不可重复读
* Write-write(WW) conflict: overwriting uncommitted data 覆盖未提交数据

### Serialisability 可串行性

就是两个事物互补干扰的样子

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-28 01.10.35.png" alt="截屏2021-07-28 01.10.35" style="zoom:50%;" />

#### Conflict Serialisability 冲突可串行

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-28 01.11.57.png" alt="截屏2021-07-28 01.11.57" style="zoom:50%;" />

### Precedence graph优先图

如果事物T1和事物T2，下图表示T1比T2先访问一个数据，所以就有T1-->T2,再T2访问数据T1访问数据就有T2-->T1，一旦成环就表示它不是一个冲突可串行化调度	

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-28 01.13.11.png" alt="截屏2021-07-28 01.13.11" style="zoom:50%;" />

#### View Serialisability 视觉可串行化、

如果俩调度满足以下三点，则它是视觉可串行化。

* 对同一 data item， 只要是有一个 schedule读了它的初始值，另外一个 schedule 也必须读它的初始值。
* 对同一data item,如果在一个 schedule 里，一个操作是读了一个写操作后的值，另一个 schedule 也必须读同样写操作后的值。
* 对同一 data item,如果在一个 schedule 里最后进行了写操作，则另一个 schedule 也要在最后进行同样的写操作。

如果三条规则都满足，才能认为两个 schedule 是视图等价的。

冲突可串行化一定是一个视觉可串行化反过来不一定

#### Recoverable Schedules



### 事务的状态

### Cascadeless Schedules 无*级联调度*	

https://blog.csdn.net/u010486124/article/details/42426127

## **Lecture 6b:** **Transaction Management – Concurrency Control** 

排他锁-- X锁

* 又称为写锁,若事物T对数据对象A加上X锁，则只允许T读取和修改A，其他任何事物都不能在对A加任何的锁，直到T释放A上的锁。

共享锁--S锁

* 又称为读锁，若事物T对数据对象A加上S锁，则其他事物只能再对A加S锁，而不能加X锁，直到T释放A上的S锁

#### dead lock

#### Two -Phase Locking Protocol 两段封锁协议

对任何数据进行读写之前，事物首先要获得对该数据的封锁

在释放一个封锁之后，事物不再获得其他封锁

* 分为两个阶段
  * 第一阶段是获得封锁，也称为扩展阶段
  * 第二阶段是释放锁，也称为收缩阶段

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-29 00.40.30.png" alt="截屏2021-07-29 00.40.30" style="zoom:30%;" />

事物2不符合两段锁协议，因为它在释放锁之后又陆续加了一堆锁

#### 两段锁协议与防止死锁的一次封锁法

* 一次封锁法要求每个事物必须一次将所有要使用的数据全部枷锁，否则就不能继续执行，因此一次封锁协法遵守两段封锁协议
* 但是两段锁协议并不要求事物必须一次将所有要使用的数据全部枷锁，因此遵守两段锁协议的事物可能发生死锁比如下图

<img src="/Users/shinbouei/Desktop/截屏2021-07-29 00.53.31.png" alt="截屏2021-07-29 00.53.31" style="zoom:40%;" />

#### Deadlock Handing 死锁处理

##### 死锁预防

##### 死锁检测（一般都是这样）

非抢占

抢占

T<sub>i</sub> -->T<sub>j</sub> 表示T<sub>i</sub>等待T<sub>j</sub>释放锁，如果成环，则表示发生死锁

死锁恢复处理：

* 选择一个victim去roll back
* Roll back 
  * total roll back
  * Partial roll back
* Starvatim:限制回滚制度



## **Lecture 6c:** **Transaction Management – Failure Recovery**

* Failure Classification
*  Storage Structure
*  Recovery and Atomicity n  Log-Based Recovery

### 可恢复的事物

T <sub>j</sub> 读T<sub>i</sub>写的事物，那么T<sub>i</sub>需要在T<sub>j</sub>之前提交.

T<sub>j</sub>在T<sub>i</sub>之前abort

比如如下调度

T1:write(X); T1:write(Y); T2:read(X); T2:write(Y); T2:abort; T1:write(Z); T1:commit; T3:read(Y); T3:write(Z); T3:commit.

解：X：W<sub>1</sub> R<sub>2</sub>

​		Y:W<sub>1</sub>W<sub>2</sub>R<sub>3</sub>

​	    Z:W<sub>1</sub>W<sub>3</sub> 

先看x，事物1先写，事物2后读，然后事物2abort了，所以x是可以恢复的

在看y：事物2先写，事物3后读，但是呢写的后面就是abort，所以看事物1和事物3的关系，观察可知，事物1先commit，事物3后commit所以可以恢复

再看z：俩写操作不考虑？

### Failure Classification

#### **Transaction failure**:

某个事物在运行过程中由于种种原因未运行至正常终点就夭折了

* **Logical errors**: transaction cannot complete due to some internal error condition
  * 业务规则要求终止，就比如余额不足，就得必须终止

* **System errors**: the database system must terminate an active transaction due to an error condition (e.g., deadlock)

 恢复技术：undo 和rollback

#### **System crash**: a power failure or other hardware or software failure causes the system to crash.

 恢复技术：

1. 清除尚未完成的事物对数据库的所有修改
   1. 系统重新启动以后，需要强行撤销(undo)所有未完成的事物
2. 将缓冲区中已完成的事物的提交结果写入数据库
   1. 系统重新启动后，需要重做(redo)所有已提交的事物

#### **Disk failure**: a head crash or similar disk failure destroys all or part of disk storage

恢复技术：更换或自动切换磁盘介质

恢复策略：

* 第一步： 创建redolist和undolist
  * 正向扫描：每读到一个事物的开始记录就将该事物加入到undo队列，每读到一个事物的结束，就将该事物从undo队列移除，如果结束标记是commit，就将该事物加入到redo队列，当扫描完日志文件之后undo队列记录了所有未完成的事物，redo队列记录了所有已成功提交的事物。
* 第二步撤销undo队列中的事物对数据库所造成的修改
  * 从日志结尾开始反向扫描即每读一个日志记录，指针反向移动一条记录，对undo队列中的每个操作做逆操作，如果修改前的记录为空，则执行delete语句，删除被插入的对象，如果修改后的值为空，则执行insert插入被删除的对象，如果修改前后值都有，则吧修改后的值改完修改前的值，如果读到了开始，则 将其从undo队列移除。重复以上操作，直到undo队列为空
* 第三步：重做redo列表中的事物
  * 从日志头开始正向扫描文件，  知道日志文件结束，或者redo列表为空。如果读到了commit标记



#### 具有检查点checkpoint的恢复技术

 ### 并发操作带来的数据不一致性

#### 丢失更新

两个以上的事物从数据库中读入同一数据并修改，其中一个事物（后提交的事物）的提交结果破坏了另一个事物（先提交的事物）的提交结果，导致先提交的事物对DB的修改丢失。（买机票） 

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210726192926670.png" alt="image-20210726192926670" style="zoom:50%;" />

#### 读脏数据

事物1修改某一数据，并将其写回磁盘，事物2读取同一数据后，事物1由于某种原因被撤销，这时事物1已修改过的数据被恢复初始值。但是事物2读到的还是修改后的数据，是不正确的数据。

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210726193426956.png" alt="image-20210726193426956" style="zoom:50%;" />

#### 不可重复读

事物1读取数据后，事物2执行更新操作，使事物1无法再显现前一次读取操作，三种情况。

* 事物2修改了事物1所读数据，当事物1再次读取数据的时候，得到与前一次不同的值。
* 事物2删除了部分记录，当事物1再次读取该数据的时候，发现某些数据消失
* 事物2插入了一些记录，当事物1再次按相同条件读取数据时，发现多了一条记录 

### 封锁

排他锁-- X锁

* 又称为写锁,若事物T对数据对象A加上X锁，则只允许T读取和修改A，其他任何事物都不能在对A加任何的锁，直到T释放A上的锁。

共享锁--S锁

* 又称为读锁，若事物T对数据对象A加上S锁，则其他事物只能再对A加S锁，而不能加X锁，直到T释放A上的S锁

#### 封锁协议

在运用X锁和S锁对数据对象进行加锁时，需要约定一些规则：封锁协议：Locking Protocol

1. 什么时候申请X锁或S锁
2. 持锁时间、何时释放

不同锁封锁协议，在不同程度上为并发操作正确调度提供了一定的保证。不同级别的封锁协议达到的**系统一致性级别**是不同的

常用的封锁协议：

#### 一级封锁协议

* 事物T在修改数据R之前必须先对其加入X锁，直到事物结束才释放
* 1级封锁协议可防止丢失更新
  * 在1级封锁协议中，如果只是读数据，是不需要加锁的，所以它不能保证可重复读和不可重复读“脏”数据

#### 二级封锁协议

* 1级封锁协议+事物T在读数据R前必须加S锁，读完后可以释放S锁

* 二级封锁协议可以防止修改和读“脏数据”如下图

  <img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-27 00.20.36.png" alt="截屏2021-07-27 00.20.36" style="zoom:50%;" />

* 在二级封锁协议中，由于读完数据后即可释放S锁，所以它不能保证可重复读，如下图

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-27 00.19.42.png" alt="截屏2021-07-27 00.19.42" style="zoom:50%;" />

#### 三级封锁协议

1级封锁协议+事物T在读取数据R前必须加S锁，直到 事物结束时才释放

三级封锁协议可以防止丢失修改，读“脏“数据以及不可重复读数据。

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/截屏2021-07-27 00.27.51.png" alt="截屏2021-07-27 00.27.51" style="zoom:50%;" />







