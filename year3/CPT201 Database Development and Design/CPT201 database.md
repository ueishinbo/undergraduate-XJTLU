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

先把这个满的节点再加上从子节点提上来的节点合并一下，然后用公式计算出要分裂的点，也就是**⌈(n+1) / 2⌉**,然后再把这个节点继续往上套，跟递归一样

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

#### **Index scan** – search algorithms that use an index

 selection condition must be on search-key of index.

比如b+树索引和hash索引



#### Algorithm for Selection Operation (File scan: *linear search*)

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
* 要记得b+树index的高度最高是**⎡log<sub>⎡n/2⎤</sub>(K)⎤** :其中n是节点的指针数量，k是节点的search key数量
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



<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210720031702239.png" alt="image-20210720031702239" style="zoom:50%;" />

* Number of records of customer: 10,000
* Number of blocks of customer: 400
* Number of records of depositor: 5,000
* Number of blocks of depositor: 100

### Nested-Loop Join

The simplest join algorithms, that can be used independently of everything (like the linear search for selection)

> To compute the theta join: r ⋈ s：
>
> **for each**tupletr **in**r**dobegin**
>
> ​	**for each tuple** ts **in** s **do begin**
>
>  		test pair (tr,ts) to see if they satisfy the join condition θ 
>
> ​		 if they do, add tr • ts to the result.
>
> ​	**end **
>
> **end**

<mark>r is called the **outer relation** and s the **inner relation** of the join.</mark>

这个贼重要，会影响结果

* 最坏的情况下， if there is enough memory only to hold one block of each relation,n<sub>r</sub> 是relation r的tuples数目。所以estimate的花费是：
  * <mark>n<sub>r</sub> * b<sub>s</sub> + b<sub>r</sub> block transfers, plus n<sub>r</sub> + b<sub>r</sub> seeks</mark>

* If the smaller relation fits entirely in memory, use that as the inner relation.(最好情况)
  * <mark>Reduces cost to b<sub>r</sub> + b<sub>s</sub> block transfers and 2 seeks</mark>

* <mark>通常来说，选取选取**较小**的关系作为**outer**的关系。</mark>
* 所以说，选择inner和outer取决于每个relation关系的szie

#### Nested-Loop Join cost example 

Assuming worst case memory availability cost estimate is

* 让depositor作为outer relation：
  * 5,000 * 400 + 100 = 2,000,100 block transfers
  * 5,000 + 100 = 5,100 seeks

* 让customer作为outer relation
  * 10,000 * 100 + 400 = 1,000,400  block transfers
  * and 10,400 seeks

### Block nested-loop join

* 最坏情况：<mark>b<sub>r </sub>* b<sub>s</sub> + b<sub>r</sub> block transfers and  2 * b<sub>r</sub> seeks</mark> 
  * Each block in the inner relation s is read once for each block in the outer relation (instead of once for each tuple in the outer relation).

最好情况(when smaller relation fits into memory)：<mark>b<sub>r</sub> + b<sub>s</sub> block transfers plus 2 seeks.</mark>

### index Nested - loop Join

* For each tuple tr in the outer relation r, use the index on s to look up tuples in s that satisfy the join condition with tuple tr.

* 最坏情况； buffer has space for only one page of r, and, for each tuple in r, we perform an index lookup on s.

* Cost of the join: <mark>b<sub>r</sub> + n<sub>r</sub> * c </mark>block transfers and seeks

  * Where c is the cost of traversing index and fetching all matching s (c也就是树的高度)

    tuples for one tuple in r

  * **c** can be estimated as cost of a single selection on s using the join condition (usually quite low, when compared to the join)

* <mark>如果两个关系上都有索引的话，一般把tuple较小的作为外层关系</mark>

* 连接时间代价是：<mark>b<sub>r</sub>(t<sub>T</sub> + t<sub>S</sub>) + n<sub>r</sub> * c</mark>

一般情况下是内层循环有索引

#### Example of Indexed Nested- Loop Join Costs

height is no more than ⌈log<sub>⌈n/2⌉</sub>(K)⌉

Compute depositor ⋈ customer, with **depositor** as the **outer** relation.

* 让customer有b+tree索引 on the join attribute customer-name, with n = 20
* indexed nested loops join的花费是：100 + 5000*（1+4） = 25100 block transfer和seek

### Merge sort join

* 只可以在等值连接和自然链接中
* merge join的花费是(B<sub>b</sub>是blocks是每个关系中分配在内存中的block数)：b<sub>r</sub> + b<sub>s</sub> block transfers +⎡b<sub>r</sub>/b<sub>b</sub>⎤+⎡b<sub>s</sub>/b<sub>b</sub>⎤ seeks
* <mark>如果这个关系没排序还得加上排序的花销</mark>

#### merge sort

merge sort 和 merge sort join不一样

Let *M* denote the number of blocks in the main memory buffer available for sorting, that is, the number of disk blocks whose contents can be buffered in available main memory.

transfer: 书上：b<sub>r</sub>(2⌈log<sub>⌊*M*∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ + 1) ttl：b<sub>r</sub>(2⌈log<sub>M-1</sub>(b<sub>r</sub>∕M)⌉ + 1)

Seek:2⌈b<sub>r</sub>∕M⌉ + ⌈b<sub>r</sub>∕b<sub>b</sub>⌉(2⌈log<sub>⌊M∕b<sub>b</sub>⌋−1</sub>(b<sub>r</sub>∕M)⌉ − 1)



### Hash index

* 也只适用于自然链接和等值连接

* A hash function h is used to partition tuples of both relations

*  The cost of hash join is

  3(b<sub>r</sub> + b<sub>s</sub>) + 4 * n<sub>h</sub> block transfers, and

  2(⎡b<sub>r</sub>/b<sub>b</sub>⎤+⎡b<sub>s</sub>/b<sub>b</sub>⎤)+2*n<sub>h</sub> seeks

* If the entire build input can be kept in main memory (then no partitioning is required), **Cost estimate goes down to br + bs and 2 seeks.**

  * b<sub>b</sub>：some blocks of memory(b<sub>b</sub>) are reserved as the output buffer for each partition.



## Week5a **Query** **Optimisation 1**

V（A,r）：关系r中属性A中出现非重复值的个数，如果A是关系r上的主码则V(A,r)等于nr



## Week5b **Query** Optimisation 2

### 代数优化的启发式规则：

* 选择运算尽量先做：减少中间集的规模
* 投影运算和选择运算同时进行：避免重复扫描
* 将投影运算与其前后的双目运算结合起来：避免重复扫描

* 某些选择运算+其前面的笛卡尔积 ==〉连接运算（减少中间集的规模）
  * σ<sub>S.<sub>sno</sub></sub> = SC.<sub>sno</sub>(S ✖️SC)  ==〉S ⋈ SC

将sql语句转换为查询树

<img src="/Users/shinbouei/Downloads/IMG_0015.jpg" alt="IMG_0015" style="zoom:30%;" />















