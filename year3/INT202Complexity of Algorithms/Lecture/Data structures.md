# Data structures
- Algorithmic computations require data (information) upon which to operate.
- The speed of algorithmic computations is (partially) dependent on efficient use of this data.
- Data structures are specific methods for storing and accessing for information.
- We study different kinds of data structures as one kind may be more appropriate than another depending upon the type of data stored, and how
we need to use it for a particular algorithm.

算法是基于数据来进行操作的，也就是说没有数据的话算法就没有意义。<br>
算法的运行时间部分取决于数据的使用效率。<br>
数据结构是一种存储和访问信息的特殊方法。<br>
++**我们学习不同种类的数据结构是为了找到一种最为合适的去储存特定的数据，并且我们需要将其如何运用到合适的算法**++

## Data Structures: Stacks
a stack is a **Last-in,First-Out**(LIFO) data structure.
- Items can be inserted into a stack at any time (assuming no stack-overflow)
- We only have direct access to the last element that was inserted.

For example, Web browsers store recently visited web addresses on a stack.<br>
栈是一种后进先出的数据结构，（类似于装羽毛球的筒，第一个从屁股插进去的，最后一个出来，球筒的口让堵死了）

- Item可以在任何时候插入（想象不会发生栈溢出的情况）
- 我们只可以直接访问插入的最后一个元素

例如：web浏览器在栈中存储最近访问的web地址。
### Stack Abstract Data Type(抽象数据类型)
a **stack** is an Abstract Data Type(ADT) and uspports the following methods:
- push(Obj):insert object Obj onto the top of the stack
- pop(): Remove(and return) the object from the top of the stack. An error occurs if th estack is empty.

In addition to push and po there are also typically method like:
- initialize():initialize a stack
- isEmpty(): returns a **true** if stack is empty, **false** otherwise.
- isFull(): returns a ture if stack is full, false otherwise.
> ADT包括数据数据元素，数据关系以及相关的操作。即：1数据对象(数据元素集合)，2数据关系（数据关系的二元结合), 3基本操作(操作函数的罗列)

### Stack:Push and Pop methods:

> push(Obj)
> check to see if stack is full
> if size() == N
> 	then indicate stack-full error occurred
> else t<--t + 1
>
> ​	S[t]<-- Obj

> Pop()
>
> Check to see if stack is empty
>
> if isEmpty()
>
> ​	then indicate "stack empty" error occurred
>
> else Obj<--S[t]
>
> ​	S[t]<--null
>
> ​	t<-- t-1
>
> Return Obj



### Stack： Application
- Important in run-time environments of modern procedural languages(e..g., c, c++, java)
- Evaluating arithmetic expressions can be performed using a stack if they are given using postifix notation (Reverse Polish notation (RPN), named for its developer Jan Lukasiewicz).
- problem:Reversing an Array

The following pseudocode shows this algorithm:
```
ReverseArray(Data: values[])
    //push the values from the array onto the stack.
    Stack:stack = New Stack
    For i = 0 To <length of value> -1
        stack.Push(value[i])
    Next i
    //Pop the items off the stack into the array.
    For i = 0 To < length of values> - 1
        values[i] = stack.Pop();
    Next i
End ReverseArray
```
- Problem:Reverse Polish notation（逆波兰表达式）

In postfix notation the operands precede the arithmetic～～~字太多了不想打了..
**大概意思就是说将运算符写在操作数之后，新建一个表达式,如果当前字符为变量或者为数字，则压栈，如果是运算符，则将栈顶两个元素弹出作相应运算，结果再入栈，最后当表达式扫描完后，栈里的就是结果。**
<br>
比如运算5 -（6+7）* 8 + 9 / 4 。它的逆波兰表达式是：5 6 7 + 8 * - 9 4 /
- Exiting a Maze.(逃出迷宫)

~~看起来太尼玛复杂了额... 优点自动机内味儿， 溜溜了~~
## Data Structures:Queues
- A queue is a **First-In, First-out** data Structure, like queues you're used to in the real world.（就像羽毛球筒一样只不过这次只能从屁股插入，从头取出）。
-  Object can be inserted(at the rear) into a queue into a queue at any time, but only the element at the front of the queue can be removed. 
-  An example of queue is a list of jobs sent to printer for printing waiting lines.
-  We say that elements enter the queue at the rear and are removed from the front.

队列，是一种先进先出的数据结构。<br>
对象可以再任何时间插入队列(屁股)，但是只有队列头部的数据可以被移除。<br>
例如：一个打印消息队列发送给打印机等待打印。<br>
我们通常说元素在屁股进入队列，在头部删除.<br>



### Queue ADT
一个ADT队列支持以下基础方法。<br>
* enqueue(Obj): 将对象(object) 插入队列的 rear
* dequeue(): 将队列的头部进行返回和删除，如果队列是空的话，将会发生错误。

除去enqueue()和dequeue()队列也有:<br>
* size(): 返回队列对象元素的数量。
* isEmpty(): 返回true如果队列为空,否则为false.
* isFull(): 返回truer如果队列为满的情况下，否则返回false.
* front(): 返回，但是不移除在队列头部的元素。如果队列为空，则返回一个error.

### Queue and Multiprogramming(队列和多道程序设计)
- Multiprogramming achieves a limited form of parallelism.
- Allows multiple tasks  or threads to be run at the same time.
- For example, a computer(or program) might use multiple thread, one of which is responsible for catching mouse clicks, whilst another may be responsible for drawing animations on the screen.
- When designing programs(or opeating systems) that use multiple threads, we must not allow a single thread to monopolize the CPU.
- One solution is to use a queue to allocate CPU time to threads in a round robin protocol. Here we can use a queue taht holds the collection of threads. The thread at the beginning of the queue is removed, allocated some portion the CPU time, and then replaced at the rear of the queue.

多道程序设计实现了并行的限制。<Br>
允许多道任务或线程在同一时间运行，<br>
例如，一个计算机(或程序)使用多线程，我们一定不能让一个线程去独占CPU。<br>
一个解决方法就是使用队列去分配CPU给循环协议上的线程。这样我们就可以使用队列去管控线程的集合。**队列头部的线程被移除，分配部分CPU时间，然后在队列的末尾进行replaed。**
### Data Structures: List ADT
- a list is a collection of items, with each item being stored in a node which contains a data field and pointer to the next element in a list.
- Data can be insert anywhere in the list by inserting a new node into the list and reassigning posinters.
- A list ADT supports: referring, update(both insert and delete) as well as searching methods.
- We can implement the list ADT as either a singly-, or doubly-linked list.

### List ADT: Referring methods:
first(): Reurn position of first element; error occures if list is empty.<br>
last(): Return the position of last element; error occures if list is empty.<br>
isFirst(P): Return true if element P is first item in list, false otherwise.<br>
isLast(P): Return true if element P is last item in list, false otherwise.<br>
before(P): Return the position of the element in S preceding the one at position p; error if P is first element.<br>
after(P):Return the position of the element in S following the one at position p; error if p is last element.
### List ADT: Update methods:
一些更新的方法，例如replace、swap、insert、remove，不想写了..在ppt27

~~后面都是再讲链表~~




## DataStructures: Rooted Trees


- A rooted tree, T, is a set of nodes which store elements in a parent-child relationship.
- T has a special node, r,called the root of T.
- Each node of T(excluding the root node r) has a parent node.

<img src="https://i.loli.net/2021/04/29/XIYio9M2JBkfQ3F.png" alt="image-20210427200039315.png" style="zoom:50%;" />

### Rooted trees: terminology

- if node u is the parent of node v, then v is a child of u.
- Two nodes that are children of the same arent are called siblings.
- A ndoe is a leaf(external) if it has no children and internal otherwise.
- A tree is ordered if there is a linear ordering defined for the children of each internal node(i.e. an internal node has a distinguished first child,second child,ect).

如果节点u是v的父节点，则v是u的子节点。<br>
具有相同父节点的两个子节点叫做siblings<br>如果一个节点没有子节点则称为leaf(external)<br>
一个树的所有的internal node如果是按顺序排列的则称这个树是有序的

### Binary Trees
- a binary tree is a rooted ordered tree in which every node has at most two chiledren.
- a binary tree is proper if each internal node has exactly two children.
- Each child in a binary tree is labeled as either a left child or a right child.

一个二叉树是一个由根节点有序排序的树每一个节点最多有两个子节点。<br>
一个二叉树是正确的如果每一个internal node都有恰好有两个子节点<br>
在二叉树中每一个子节点被标记为左节点或右节点。<br>
### Trre ADT Methods
Tree ADT access methods:
- root():return the root of the tree.
- parent(v): return parent of v.
- children(v):return links to v's children.

Tree ADT query methods:
- isInternal(v):test whether vis internal node.
- isExternal(v):test whether v is external node.
- isRoot(v):test whether vis the root.

Tree ADT generic meethods:
- size(): return the number of modes in the tree.
- elements(): return a list of all elements.
- positions(): return a list of addresses of all elements.
- swapElements(u,v):swap elements stored at positions u and v.
- replaceElements(v,e): replace element at address vwith element e.

### Depth of a node in a tree
The depth of a node,v, is number of ancestors of v, excluding v itself. This is easily computed by a recurisive funciton.<br>
Depth(T,v)
> DEPTH(T,v)
>
> ​	if T.isRoot(v)
>
> ​		then return 0
>
> ​	else return 1+ DEPTH(T,T.parent(v))	


v节点的深度，是由v节点的祖先数量来标记的(但不包括自身)，用递归计算很方便～
### Height of a tree
The height of a tree is equal to the maximum depth of an external node in it. the following psudo-code computes the height of the subtree rooted at v.

```
HEIGHT(T,v)
if isEXTERNAL(T,v)
    then return 0
    else
        h = 0
        for each w ∈ T.CHILDREN(v)
            do
                h = MAX(h,HEIGHT(T,w))
        return 1+h
```
### Tree Traversal
- in a traversal, the goal is for the algorithm to visit all the nodes in the tree in some order and perform an operation on them.
- Traversal and Searching
- Binary trees have three kinds of traversals: preorder, postorder, and inorder.
- 遍历 算法的目的是以某种顺序浏览树中的所有节点
- 二叉树树有三种遍历方式：前序遍历、中序遍历、后序遍历

### Preorder traversal in trees (前序遍历)
- a traversal visits the nodes of a tree in a systematic manner
- In a preorder traversal, a node is visited before its descendants
- application: print a structured document
- 

<img src="https://i.loli.net/2021/04/29/DWBEjlKP1hXwC4T.png" alt="image-20210427201833151.png" style="zoom:50%;" />

> Alorithm preOrder(v)
>     visit(v)
>     for each child w of v
>         preOrder(w)

<img src="https://i.loli.net/2021/04/29/RFyUYZSkTfB2brz.png" alt="image-20210427202318168.png" style="zoom:50%;" />

## Postorder traversal （后序遍历）

```
Alorithm postorder(v)
    for each child w of v
        postorder(w)
    visit(v)
```
<img src="https://i.loli.net/2021/04/29/I3SfMOPoirTRAD7.png" alt="image-20210427202905793.png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/29/XtBkON2R3ZpDC5V.png" alt="image-20210427203630973.png" style="zoom:50%;" />

### inorder traversal in trees（中序排列）

```
Alorithm inOrder(v)
    if hasLeft(v)
        inOrder(left(v))
    visit(v)
    if hasRight(v)
        inOrder(right(v))
    
```



### ![![image-20210427213841724.png](https://i.loli.net/2021/04/29/jrDVEivwtMexgop.png)](/Users/shinbouei/Library/Application Support/typora-user-images/image-20210427213841724.png)

<img src="https://i.loli.net/2021/04/29/bIMKJn9v5fEumsH.png" alt="image-20210427213912667.png" style="zoom:50%;" />

---

