# Search Algorithm

## Sorting

Sorting problem: Given a collection, C, of n elements (and a total ordering) arrange the elements of C into non-decreasing order, e.g

<img src="https://i.loli.net/2021/05/10/gWpyKXf9CDxeLwG.png" alt="WX20210510-204830@2x.png" style="zoom:30%;" />

Sorting is a fundamental algorithmic problem in computer science.

We wil investigate various methods that we can use to sort items.

Many algorithms perform sorting(as a subroutine) during their execution. Hence, efficient sorting methods are crucial to achieving good algorithmic performance.

We may not always require a fully sorted list, so some methods might be more appropriate depending upon the exact task at hand.

Sorting algorithms might be directly adaptable to perform additional tasks and diretly provide solutions in this fashion.

## Priority Queues （优先队列）

A Priority Queue is a container of elements, each having an associated key.

Keys determine the priority used in picking elements to be removed.

A priority Queue(PQ) has these fundamental methods:

* insertItem(k,e): insert element e having key k into PQ.
* removeMin():minimum element.
* minElement(): return minimum element.
* minKey(): return key of minimum element.

一个优先队列是元素的容器，每个元素有一个关联键。这个关联键通常用来确定元素的优先级以便于哪个元素去删除

### PQ Sorting - Algorithm

How can we use a priority queue to perform sorting on a set C?

Do this in two phases:

* First phase: Put elements of C into a initially empty priority queue, P by a series of n insertItemoperations.
* Seconde phase: Extract the elements from P in non-decreasing order using a series of n removeMinoperations.

## Heap Data Structure.

A heap is a realization of Priority Queue that is efficient for both insertions and deletions,
A heap allows insertions and deletions to be performed in logarithmic time.
In a heap the elements and their keys are stored in an almost **complete binary tree.** Even level of the binary tree, except possibly the last one, will have the maximum number of children possible.

堆实现了优先队列并且高效的实现了插入和删除. 堆允许插入和删除以对数时间去执行. 在堆中元素和他们的key存储在一个完全二叉树上。二叉树的每一层，除去最后一次，尽可能会有多的孩子

Complete Binary Tree

here are two important types of binary trees. Note that the definitions, while similar, are logically independent.

**definition：** a binary tree T is full if each node is either a leaf or pssesses exactly two child nodes.

**definition：** a binary tree T with n levels is complete if all levels except possibly the last are completely full, and the last level has all its nodes to th eleft side.

 full tree：节点要么为空，要么只有两个节点
Complete Binary Tree: 如果树的深度是k，除了k层以外都是全满的，第k层所有节点都连续集中在最左边。～

<img src="https://i.loli.net/2021/05/10/k4VC53LxY21h967.png" alt="WX20210510-211250@2x.png" style="zoom:30%;" />

A heap is a binary tree storing key at its internal nodes and satisfying the following properties:

* Heap-Order: for every internal node v other than the root, key(v) >= key(parent(v))

<img src="https://i.loli.net/2021/05/10/Y4QXGHcJLKljR1Z.png" alt="WX20210510-211753@2x.png" style="zoom:40%;" />

Binary heap: Array representation of a heap -ordered complete binary tree.

Heap-ordered binary tree.

* keys in nodes
* Parent's key no smaller than children's key

Array representation:

* Indices start 1.
* Take nodes in level order.
* No explicits links needed

An efficient realization of a heap can be achieved using an array for storing the elements.

For any given node at position i:

* Its **Left Child** is at [2 * i] if available.
* Its **Right Child** is at [2 * + 1]
* its **Parent Node** is at [⌊i / 2⌋]

<img src="https://i.loli.net/2021/05/10/279gl1dk4sJGtOI.png" alt="WX20210510-230756@2x.png" style="zoom:50%;" />

堆分为两种：最大堆和最小堆，两者的差别在于节点的排序方式。

在最大堆当中，父节点的值比每一个子节点的值都要大。在最小堆中，父节点的值比每一个子节点的值都要小。这就是所谓的**堆属性**，并且这个属性对堆中的每一额节点都成了。

例如：

<img src="https://static01.imgkr.com/temp/dd9a982c2f494755b465d93922c0575b.png" alt="WX20210510-230756@2x.png" style="zoom:70%;" />

这是一个最大堆，因为每一个父节点的值都要被其子节点要打。10比7和2都大，7比5个1都大。

根据这一属性，哪么最大堆总是将其中最大值存放在树的根节点。而对于最小堆，根节点中的元素总是树中的最小值。堆的属性非常有用，因为堆常常被当做优先队列使用，因为可以快速地访问到**最重要**的元素。

> **注意：**堆的根节点存放的是最大元素或者是最小元素，但是其他节点的排序顺序是未知的。例如，在一个最大堆中，堆大的那一个元素总是位于index0的位置，但是最小的元素**未必**是最后一个元素。
>
> 唯一能确定的是最小的元素是一个叶节点。但是不确定是哪一个。

#### 堆和普通树的区别。

堆并不能取代二叉搜索树，他们之间有相似之处也有一些不同之处：

* 节点的顺序：在二叉搜索树中，左子节点必须比父节点小，右子节点必须比父节点大。但是在堆中并非如此。在最大堆中两个子节点都必须比父节点小。而在最小堆中，他们都必须比父节点大。
* 内存占用：普通树占用的内存空间比他们存储的数据要多。你必须节点对象以及左右子节点指针分配内存。而堆仅仅使用一个数组来存储数组，而不使用指针。
* 平衡：二叉搜索树必须是平衡的情况下，其大部分操作的复杂度才能达到O(log n). 你可以按任意顺序位置插入/删除数据，或者使用AVL树或者红黑树，但是在堆中实际上不需要整棵树都是有序的。我们只需要满足堆属性即可，所以在堆中平衡不是问题，因为堆中数据的组织方式可以保证O(log n)的性能。
* 搜索：在二叉树中搜索会很快，但是在堆中搜索会很慢，在堆中搜索不是第一优先级，因为使用堆的目的是将最大((或者最小)的节点放在最前面，从而快速的进行相关插入、删除操作。

#### 来自数组的树

用数组来实现树的相关数据结构也许看起来有点古怪，但是它在实施将和空间上都是很高效的。

我们准备将上面的树这样存储：

```java
[ 10, 7, 2, 5, 1 ]
```

我们除了一个简单的数组以外，不需要任何额外的空间。

如果我们不允许使用指针，那么我们怎么知道哪一个节点是父节点，哪一个节点是它的子节点？答：节点在数组中的位置index和它父节点以及子节点之间的索引之间有一个映射关系。

如果<mark>i</mark>是节点的索引，那么下面的公式就给出了它父节点和子节点在数组中的位置：

```java 
parent(i) = floor((i - 1)/2)
left(i)   = 2i + 1
right(i)  = 2i + 2
```

注意<mark>right(i)</mark>就是简单的<mark>left(i) + 1</mark>点总是处于相邻的位置。

我们可以将公式写到前面的例子中验证一下。

| Node | Array index | Parent index(i | Left child | Right child |
| ---- | ----------- | -------------- | ---------- | ----------- |
| 10   | 0           | -1             | 1          | 2'          |
| 7    | 1           | 0              | 3          | 4           |
| 2    | 2           | 0              | 5          | 6           |
| 5    | 3           | 1              | 7          | 8           |
| 1    | 4           | 1              | 9          | 10          |

> **注意：**根节点(10)没有父节点，因为-1不是一个有效的数组索引。同样，节点(2),(5)和(1)没有子节点，因为这些索引已经超过了数组的大小，所以我们在使用这些索引值的时候需要保证是有效的索引值。

复习一下，在最大堆中，父节点的值总是要大于(或者等于)其子节点的值，这意味着下面的公式堆数组中的任意一个索引i都成立：

```java
array[parent(i)] >= array[i]
```

可以用上面的例子来验证一下这个堆属性。

如你所见，这些公式允许我们**不使用指针**就可以找到任何一个节点的父节点或者子节点。事情比简单的去掉指针要复杂，但这就是交易：我们节约了空间，但是要进行更多的计算。新号这些计算很快并且只需要只需要O(1)的时间。

理解数组索引和节点位置之间的关系非常重要。这里有一个更大的堆，它有15个节点被分成了四层

<img src="https://i.loli.net/2021/05/11/QDjMNa3Z2EfcbqA.png" alt="WX20210511-112130@2x.png" style="zoom:50%;" />

<mark>**图片中的数字不是节点的值，而是储存这个节点的数组索引，这里是数组索引和树的层级之间的关系：**</mark>

<img src="https://i.loli.net/2021/05/11/i74O1DGgXjxHI96.png" alt="WX20210511-112704@2x.png" style="zoom:50%;" />

由上图可以看到，数组中父节点总是在子节点的前面。

注意这个方案与一些限制。你可以在普通二叉树中按照下面的方式组织数据，但是在堆中不可以

<img src="https://i.loli.net/2021/05/11/ZkvKnHhfocWzRlN.png" alt="WX20210511-113048@2x.png" style="zoom:50%;" />

在堆中，当前层级所有的节点都已经填满之前不允许开始下一层的填充，所以堆总是有这样的形状

<img src="https://i.loli.net/2021/05/11/e6Gvd5uW2Rjz9VY.png" alt="WX20210511-113238@2x.png" style="zoom:50%;" />

小测验：假设我们有这样一个数组：

```java
[ 10, 14, 25, 33, 81, 82, 99 ]
```

这是一个有效堆吗？确实。一个从低到高有序排列的数组是以有效的最小堆，我们可以将这个堆画出来。

<img src="https://i.loli.net/2021/05/11/OV9dmkp38MFCaNS.png" alt="WX20210511-113543@2x.png" style="zoom:50%;" />

堆属性使用与每一个节点，因为父节点总是比它的子节点小。（你也可以验证一下：一个从高到低有序排列的数组是一个有效的最大堆）

> 注意：并不是每一个最小堆都是一个有序数组，要将堆转换成有序数组，需要使用堆排序。

如果一个堆又n个节点，那么它的高度是*h = floor(log2(n))*。这是因为我们总是要将这一层完全填满以后才会填充新的一层。上面的例子有 15 个节点，所以它的高度是 `floor(log2(15)) = floor(3.91) = 3`。



如果最下面的一层已经填满，那么那一层包含 *2^h* 个节点。树中这一层以上所有的节点数目为 *2^h - 1*。同样是上面这个例子，最下面的一层有8个节点，实际上就是 `2^3 = 8`。前面的三层一共包含7的节点，即：`2^3 - 1 = 8 - 1 = 7`。

所以整个堆中的节点数目为：* 2^(h+1) - 1*。上面的例子中，`2^4 - 1 = 16 - 1 = 15`



叶节点总是位于数组的 *floor(n/2)* 和 *n-1* 之间。

#### 可以用堆来做什么

有两个原始操作用于保证插入或 删除节点以后堆是一个有效的最大堆或者最小堆：

* `shifUp()`: 如果一个节点比它的父节点大（最大堆）或者小（最小堆），那么需要将它同父节点交换位置。这样是这个节点在数组的位置上升。
* `shiftDown()`: 如果一个节点比它的子节点小（最大堆）或者大（最小堆），那么需要将它向下移动。这个操作也称作“堆化（heapify）”。

shiftUp 或者 shiftDown 是一个递归的过程，所以它的时间复杂度是 **O(log n)**。



基于这两个原始操作还有一些其他的操作：

- `insert(value)`: 在堆的尾部添加一个新的元素，然后使用 `shiftUp` 来修复对。
- `remove()`: 移除并返回最大值（最大堆）或者最小值（最小堆）。为了将这个节点删除后的空位填补上，需要将最后一个元素移到根节点的位置，然后使用 `shiftDown` 方法来修复堆。
- `removeAtIndex(index)`: 和 `remove()` 一样，差别在于可以移除堆中任意节点，而不仅仅是根节点。当它与子节点比较位置不时无序时使用 `shiftDown()`，如果与父节点比较发现无序则使用 `shiftUp()`。
- `replace(index, value)`：将一个更小的值（最小堆）或者更大的值（最大堆）赋值给一个节点。由于这个操作破坏了堆属性，所以需要使用 `shiftUp()` 来修复堆属性。

上面所有的操作的时间复杂度都是 **O(log n)**，因为 shiftUp 和 shiftDown 都很费时。还有少数一些操作需要更多的时间：

- `search(value)`:堆不是为快速搜索而建立的，但是 `replace()` 和 `removeAtIndex()` 操作需要找到节点在数组中的index，所以你需要先找到这个index。时间复杂度：**O(n)**。
- `buildHeap(array)`:通过反复调用 `insert()` 方法将一个（无序）数组转换成一个堆。如果你足够聪明，你可以在 **O(n)** 时间内完成。
- 堆排序：由于堆就是一个数组，我们可以使用它独特的属性将数组从低到高排序。时间复杂度：**O(n lg n)**。

堆还有个`peak()`方法，不用删除节点就返回最大值(最大堆)或者最小值(最小堆)。时间复杂度为O(1)

#### 插入

我们通过一个插入例子来看看插入操作的细节，我们将数字16插入到这个堆中：

<img src="https://i.loli.net/2021/05/11/P69dJNm1AQiktaF.png" alt="WX20210511-123158@2x.png" style="zoom:50%;" />

堆的数组是： `[ 10, 7, 2, 5, 1 ]`

第一步是将新的元素插入到数组的尾部。数组变成：

```java
[ 10, 7, 2, 5, 1, 16 ]
```

<img src="https://i.loli.net/2021/05/11/VJpHEBxj28XhYUG.png" alt="WX20210511-125441@2x.png" style="zoom:50%;" />

16被添加到最后一行的第一个空位

但是，现在堆属性不满足，因为**2**在**16**的上面，我们需要将大的数字放在上面因为这是一个最大堆

为了恢复堆属性，我们需要交换**16**和**2**

<img src="https://i.loli.net/2021/05/11/XPLDUCKkrolSqE4.png" alt="WX20210511-125711@2x.png" style="zoom:50%;" />

现在还没有完成，因为**10**也比**16**小，我们继续交换我们插入的元素和他的父节点，直到它的父节点比他大或者我们达到了树的顶部。这就是所谓的<mark>**shift-up**</mark>, 每一次插入操作后都需要进行。他将一个太大或者太小的数字“上浮”到树的顶部。

最后我们得到的堆是：

<img src="https://i.loli.net/2021/05/11/QuKDofNpm4VrWB2.png" alt="WX20210511-130649@2x.png" style="zoom:50%;" />

现在每一个父节点都比它的子节点大。

#### 删除根节点

我们将这个树中的(10)进行删除：

<img src="https://i.loli.net/2021/05/11/QaAHB5Vh1wvitok.png" alt="WX20210511-130828@2x.png" style="zoom:50%;" />

现在顶部有一个空的节点，怎么处理？

<img src="https://i.loli.net/2021/05/11/aW4VsYg8wU71kqE.png" alt="WX20210511-131039@2x.png" style="zoom:50%;" />

当插入节点的时候，我们将新的值返回给数组的尾部。现在我们来做相反的事情：我们取出数组中的最后一个元素，将它放到树的顶部，然后再修复堆的属性。

<img src="https://i.loli.net/2021/05/11/y3vJWG9zVMliDoB.png" alt="WX20210511-132053@2x.png" style="zoom:50%;" />

现在来看怎么 **shift-down** `(1)`。为了保持最大堆的堆属性，我们需要树的顶部是最大的数据。现在有两个数字可用于交换 `7` 和 `2`。我们选择这两者中的较大者称为最大值放在树的顶部，所以交换 `7` 和 `1`，现在树变成了：

<img src="https://i.loli.net/2021/05/11/apDsC4n6zljVPub.png" alt="WX20210511-132234@2x.png" style="zoom:50%;" />

然后继续堆化知道该节点没有任何子节点或者它比两个子节点都要大为止。对于我们的堆，我们只需要再有一次交换就恢复了堆的属性。

#### 删除任意节点

绝大多数的时候你需要删除的是堆的根节点，因为这就是对堆设计的用途。

但是，删除任意节点也很有用。这是 `remove()` 的通用版本，它可能会使用到 `shiftDown` 和 `shiftUp`。

我们还是用前面的例子，删除 `(7)`:

```java
[ 10, 7, 2, 5, 1 ]
```

你知道，移除一个元素会破坏最大堆或者最小堆属性。我们需要将删除的元素和最后一个元素互换。

```java
[ 10, 1, 2, 5, 7 ]
```

最后一个元素就是我们需要返回的元素：然后调用`removeLast()` 来将它删除。 `(1)` 比它的子节点小，所以需要 `shiftDown()` 来修复。

然而，shift down 不是我们要处理的唯一情况。也有可能我们需要 shift up。考虑一下从下面的堆中删除 `(5)` 会发生什么：

<img src="https://i.loli.net/2021/05/11/g5rk6X3JnZmq4Hv.png" alt="WX20210511-133023@2x.png" style="zoom:50%;" />

现在 `(5)` 和 `(8)` 交换了。因为 `(8)` 比它的父节点大，我们需要 `shiftUp()`。



### MergeSort

### QuickSort Tree







































