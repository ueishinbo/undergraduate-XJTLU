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