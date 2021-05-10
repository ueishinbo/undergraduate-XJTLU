## Trees

- linked struct: each node v of T is represented by an object with references to the element stored at v and posistions of ites parents and children.

  linked struct: 树T的每一个节点v储存着其父或子的指针

  <img src="https://i.loli.net/2021/04/29/HrsbGSIy8ovw6im.png" alt="image-20210427214743535.png" style="zoom:50%;" />

- For rooted trees where each node has at most t children, and is of bounded depth, you can store the tree in an array A.

  对于rooted tree 每一个节点最多含有 t个孩子，并且你可以存储这个树再任意的数组A

- Consider, for example, a binary tree. The root is stored in A[0]. The (possibly) two children of the root are stored in A[1] and A[2]. The two children of A[1] are stored in A[3] and A[4], and the two children of A[2] are in A[5] and A[6], and so forth.

   想象，如果一个二叉树，根节点储存在A[0]，根节点的两个字节点储存在 A[1]和A[2],A[1]的两个子节点储存在A[3]和A[4]，A[2]的两个子节点储存在A[5],A[6],如此类推

- In general, the two children of node A[i] are in A[2✖️i+1] and A[2✖️i+2].

  通常来说对于节点A[i]它的两个子节点分别储存在A[2*i + 1]和A[2 * i + 2]上

- The parent of node A[i](except the root) is the node in position A[⌊(i-1)/2⌋].

  对于节点A[i]来说，它的父节点储存在 A[⌊(i-1)/2⌋]上

- This can be generalized to the case when each node has at most t children.

  

### Ordered Data

- We often wish to store data that is ordered in some fashion (typically in numeric order, or alphabetical order, but there may be other ways of ordering it).
- Here we study a few methods for storing such ordered data, and maintaining the order as we add more data or remove it.
- In later lectures we will discuss efficient methods for sorting data into such an ordered collection. In these lecture notes we talk about methods for maintaining ordered data as we store it (which is different from sorting the data after we have already received the aggregated data as input).

通常情况下我们希望存储的数据以一些好用的顺序例如从小到大的数字顺序，或者从小到大的字母顺序。<br>
这里我们将学习一些方法去以顺序存储数据，并且维护顺序即便你加了数据或者删除了数据。<br>
后面的lec我们将讨论一些有用的排序方法，例如rodered collection.

### Ordered Dictionary

in an ordered dictionary, we wish to perform the usual dictonary operation:

- findElement(k): position k
- insertElement(k,e) position k, element e
- removeElement(k): position k

An ordered dictionary maintains an order relation for its elements, where the items are ordered by their keys.

### Sorted Tables

if a dictionary D, is ordered, we can store its items in a vector, S, by **non-decreasing** order of keys.(this generally assumes taht we're not going to add more items into the dictionary.)<br><br>
==还有一些..感觉没啥用 在L5ppt7页==

### binary Search（二分法搜索）

> BinarySearch(S,k,low,high)
>
> ​	//Input is an <u>order</u> array of elements
>
> ​	//Output: Element with key k if it exists, otherwise an error.
>
> If low > high
>
> ​	then return NO_SUCH_KEY			//Not present
>
> else
>
> ​	mid <--mid = ⌊(low + high) / 2⌋
>
> ​	if k = key(mid)
>
> ​		then return elem(mid)				//Found it
>
> ​	else if k < key(mid)				
>
> ​		then return BinarySearch(S,k,low,mid-1)	//try bottom 'half'
>
> ​	else return BinarySearch(S,k,mid+1,high)		// try top 'half'

<img src="https://i.loli.net/2021/05/04/xwkSU3Ace6njTqd.jpg" alt="1620104706898.jpg" style="zoom:67%;" />

### binary Search Tree(二叉查找树)

A binary search Tree(BST) applies the motivation of binary search to a tree-base data structure.

In a BST each internal node stores an element , e(or, more generally, a key k which defines the ordering, and some element e)

A BST has teh property that, given a node v storing the element e, all elenents in the left sebtree at v are less than or equal to e, and those in the right subtree at v aree geater than or equal to e.

对于某一节点v， 其左子树的值一定小于v，而右子树的值一定大于v

<img src="https://i.loli.net/2021/05/08/3ev5OXCcsM4R7qL.png" alt="WX20210508-210046@2x.png" style="zoom:50%;" />

> ​								Inorder traversal(中序遍历) of a BST:1,3,4（non-decreasing order)

To earch for a key, we trace a downward path starting at the root.

The next node visited depends on the outcome of the comparison of k with the key of the current node.

if we reach a leaf, the key is not found and we return N-SUCH-KEY

> Algorithm findElement(k,v) //k为要查找的元素,v为节点
>
> ​	if T.isElement(v)
>
> ​		return No_SUCH_KEY
>
> ​	if k < key(v)
>
> ​		return findElement(k,T.leftChild(v))
>
> ​	else if k = key(v)
>
> ​		return element(v)
>
> ​	else k > key(v)
>
> ​		return findElement(k,T.rightChild(v))

​	<img src="https://i.loli.net/2021/05/08/6yeRI9bT2wW4inC.png" alt="WX20210508-212702@2x.png" style="zoom:50%;" />

> ​             	 		example: findElement(4)

#### Time Complexity

How long doees it takes in a n element tree?

<img src="https://i.loli.net/2021/05/08/PQ5sx3CTVYpOZFf.png" alt="WX20210508-213058@2x.png" style="zoom:40%;" />

#### Insertion in a BST

* To perform operation insertItem(k,o), we search for k

* Assume k is not already in the tree, and let w be the left reached by the search

* We insert k at node w and expand w into an internal node

  

<img src="https://i.loli.net/2021/05/08/gxHhZ4MfJlVsOSn.png" alt="WX20210508-222959@2x.png" style="zoom:33%;" />

<img src="https://i.loli.net/2021/05/08/TMUdEDCIrGzLojA.png" alt="WX20210508-223031@2x.png" style="zoom:33%;" />

<img src="/Users/shinbouei/Library/Application Support/typora-user-images/image-20210508223436394.png" alt="image-20210508223436394" style="zoom:33%;" />

> ​																				Insert 5

#### Deletion in a BST

* The following algorithm for deletion has the advantage of minimizing restructuring and unbalancing of the tree. The method return the tree that results.

  1. Find the node to be removed. We'll call it *remNode*.

  2. if it's a leaf, remove it immediately by returning null.

  3. if it has only one child, remove it by returning the other child node.

  4. Otherwise, remove the <mark>inorder successor</mark> of *remNode*., copy its key into remNode, and return remNode.

     (Inorder successor: the node that would appear after the remNode if you were to do an inorder traversal of the tree)

删除节点存在三种情况：

1. 没有左右左右节点的，可以直接删除。

2. 存在左节点或者右节点的，删除后需要对子节点移动。

3. 同时存在左右子节点，不能简单的删除，但是可以通过和后继节点交换后转换为前两种情况。

   > 实际上在三种情况中，还有一个特例就是删除根节点，后续代码会有处理）

下面，我们使用图来详细解释怎么删除。

初始状态如图下琐事，我们可以按照 50, 30, 80, 20, 35, 34, 32, 40, 70, 75, 100的顺序插入到图中，就会产生下图所示的树。

<img src="https://i.loli.net/2021/05/08/ulnjNAX9hUvLm3i.png" alt="WX20210508-233239@2x.png" style="zoom:50%;" />

##### 1.没有左右节点时

在我们图中，符合这个条件的有20,32,40,75,100,我们以20来演示删除该节点

<img src="https://i.loli.net/2021/05/08/OdXwREjbyPqtCv2.png" alt="WX20210508-233555@2x.png" style="zoom:50%;" />



这种情况是最简单的，我们只需要删除该节点和父节点的关系即可。删除的时候需要先判断自己和父节点的关系是左侧还是右侧，判断方式很简单，如下:

```java
//这里忽略了父节点不存在的情况，最后会巧妙的处理这种情况
if(node.parent.left == node){
	node.parent.left = null;
}else{
  node.parent.right = null;
}
```

如果父节点的左节点是自己，就清左侧，否则就是右侧，删除后如下图所示：

<img src="https://i.loli.net/2021/05/08/yrgu7RQ6oh4JHTf.png" alt="WX20210508-234521@2x.png" style="zoom:50%;" />

##### 2. 存在左节点或者右节点时

满足这个情况的节点有34,70两个节点，这里以70为例,如下图所示：

<img src="https://i.loli.net/2021/05/08/qS5jKsLByFtpoMW.png" alt="WX20210508-234817@2x.png" style="zoom:50%;" />

删除70的时候需要断两个关系，然后建立父节点和子节点的关系，代码如下：

```java
//先找到子节点，不需要管他是左还是右
BSTNode<T> child = null;
if(node.left != null){
  child = node.left;
}else{
  child = node.right;
}
//这里忽略了父节点不存在的情况，最后会巧妙的处理这种情况
//将副节点和子节点建立联系。
```

经过上述操作后，节点状态如下图所示：

<img src="https://i.loli.net/2021/05/08/vTgYBaEMHVr5LiA.png" alt="WX20210508-235817@2x.png" style="zoom:50%;" />

##### 3.同时存在左右子节点

满足同时存在左右节点的有50,30,80,35这四个节点，30看起来更复杂，我们以30为例。

当二叉查找树以中序遍历时，遍历结果时一个从小到大排列的顺序，如下图所示.

<img src="https://i.loli.net/2021/05/09/5ivhgO3UQKNrSMX.png" alt="WX20210509-000134@2x.png" style="zoom:50%;" />

当我们删除30节点的时候，整个中序遍历的结果中，从32开始都往前移动了一位。32时30的后继节点，就是比30大的节点中最小的节点。当某个节点存在有节点的时，后继节点就是右节点中的最小值，由于左侧节点总比右侧节点和父节点小，所以后继节点一定没有左节点。从这一特点就能看出来，后继节点有可能存在于右节点，也有可能没有任何节点。后继节点还有一个特点，就是他比30的左节点大，比30所有的右节点都小，因此删除30的时候，可以直接将后继节点32的值(<mark>key</mark>)转移到30节点上，然后删除后继节点32.由于后继节点最多只有一个子节点，因此删除后继节点时，就变成了三种情况的前两种，图片所示：

<img src="https://i.loli.net/2021/05/09/aOhqe48Vr6lNbdu.png" alt="WX20210509-001345@2x.png" style="zoom:50%;" />

转移节点值的代码很容易：

```java
//获取当前节点的后继节点
Node<T> successor = successor(node);
//转移植
node.key = successor.key;
//后继变成删除，successor,就变成了前两种情况
//在图示例子中,就是第一种没有子节点的情况
node = successor;
```

##### 整合三种情况的删除

代码如下：

```java
private BSTNode<T> delete(BSTNode<T> node) {
    //第 3 种情况，如果同时存在左右子节点
    if (node.left != null && node.right != null){
        //获取后继结点
        BSTNode<T> successor = successor(node);
        //转移后继结点值到当前节点
        node.key = successor.key;
        //把要删除的当前节点设置为后继结点
        node = successor; //关键（uei）
    }
    //经过前一步处理，下面只有前两种情况，只能是一个节点或者没有节点
    //不管是否有子节点，都获取子节点
    BSTNode<T> child;
    if (node.left != null)
        child = node.left;
    else
        child = node.right;
    //如果 child != null，就说明是有一个节点的情况    
    if (child != null)
        //将子节点和父节点关联上
        child.parent = node.parent;
    //如果当前节点没有父节点（后继情况到这儿时一定有父节点）
    //说明要删除的就是根节点
    if (node.parent == null)
        //根节点设置为子节点
        //按照前面逻辑，根只有一个或者没有节点，所以直接赋值 child 即可
        mRoot = child;
    else if (node == node.parent.left)//存在父节点，并且当前节点是左节点时
        //将父节点的左节点设置为 child
        node.parent.left = child;
    else//右节点时
        //将父节点的右节点设置为 child
        node.parent.right = child;
    //返回被删除的节点
    return node;
}
//删除指定的值
public void delete(T key) {
    //获取要删除的节点
    BSTNode<T> node = search(mRoot, key);
    //如果存在就删除
    if (node != null)
       delete(node);
}
```

通过前面的铺垫和这里的代码注释，删除这个操作应该能真正的领会了，下面针对删除，完整的写了一遍

```java
/*
 * 删除结点(z)，并返回被删除的结点
 *
 * 参数说明：
 *     bst 二叉树
 *     z 删除的结点
 */
private BSTNode<T> remove(BSTree<T> bst, BSTNode<T> z) {
    //这里没起个好名字，让人看着默默奇妙，实际上 x 就是子节点 child
    BSTNode<T> x=null;
    //这里的 y 节点就是要删除的节点 delete
    BSTNode<T> y=null;
    //这个写法理解比较绕，不如反转后容易理解
    //只有一个节点或者没有节点时
    if ((z.left == null) || (z.right == null) )
        //z 就是要删除的节点
        y = z;
    else
        //当有两个子节点时，删除后继结点
        y = successor(z);
    //获取子节点，不管是左是右
    if (y.left != null)
        x = y.left;
    else
        x = y.right;
    //如果存在子节点，就关联被删节点的父节点
    if (x != null)
        x.parent = y.parent;
    //如果父节点是空，说明要删的是根节点
    if (y.parent == null)
        //设置根为 child（此时根只有一个或没有节点）
        bst.mRoot = x;
    else if (y == y.parent.left)//要删的是左节点
        y.parent.left = x;//左节点关联子节点
    else//要删的是右节点
        y.parent.right = x;//右节点关联子节点
    //如果要删的节点和一开始传入的不一样，就是后继的情况
    if (y != z)
        z.key = y.key;//后继的值传给本来要删除的节点
    //返回被删除的节点
    return y;
}

/*
 * 删除结点(z)，并返回被删除的结点
 *
 * 参数说明：
 *     tree 二叉树的根结点
 *     z 删除的结点
 */
public void remove(T key) {
    BSTNode<T> z, node;

    if ((z = search(mRoot, key)) != null)
        if ( (node = remove(this, z)) != null)
            node = null;
}
```

#### BST Performance

* Consider a dictionary with n items implemented by means of a binary search tree of height h
* The space used is O(n)
* method findElement take O(h)
  * the heighu h is <mark>O(n)</mark> in the worst case and <mark>O(log n)</mark> is hte bset case.

想象一个具有n项的dictionary，该字典是通过高度为h的BST实现的，时间复杂度最好的情况是O(n)最坏的情况是O(log n)

<img src="https://i.loli.net/2021/05/09/7TCxwsRbHKulcBa.png" alt="WX20210509-214055@2x.png" style="zoom:40%;" />

理解前面的代码后，再看上面这段代码也不难理解，所有代码中都没有处理node节点的上下级关系，因为通过其他节点已经无法引用到该<mark>node</mark>节点了所以<mark>node</mark>能被GC正常回收

#### full binary tree

==a binary tree T is full if each node is either a leaf or possesses exactly two childnodes.==
意思就是说，每一个节点要嘛是叶节点，要嘛刚好只有两个子节点。

### AVL tree(平衡二叉树的一种)

- Height-balance property: for any node n, the heights of n's left and right subtrees can differ by at most .
  **Theorem1:** the highte of an AVL tree storing n keys is O(log n).
- 对于任意节点，它的左子节点和右子节点的高度差不能超过1
- proof: n(h) the minimum number of internal nodes of an AVL tree of height h.
- - we easily see that n(1) = 1 and n(2) = 2
- for n > 2 and AVL tree of height h contains the root node, one AVL subtree of height h-1 and another of height h-2.
- That is, n(h) = 1 + n(h-1) + n(h-2)
- knowing n(h-1) > n(h-2), we get n(h) > 2n(h-2).so **n(h) > 2n(h-2), n(h-2) > 2n(h-4),**
- Solving the base case we get: n(h) > 2<sup>h/2-1</sup>, ==>h-2i = 1 or 2, depending on if h is even or odd:i = [h/2](取上整）-1. <br> Taking lograithms:h < 2logn(h) + 2 ==>logn(h) > log2<sup>h/2-1</sub>,log n(h) > h/2-1

**上面就讲了证明平衡二叉树的bigO是(logn)**<br>

An AVL tree is a tree that has the **Height-Balance Porperty**

- **Theorem:** the height of an AVL tree storing n key is O(logn)
- Consequence 1: A search in an AVL tree can be performaed in time O(log n).
- Consequence 2: Insertions and removals in AVL need more careful implementations(using ratations to maintiain the height-balance property.)

#### 平衡因子

某节点的左子树与右子树的高度（深度）差即为该节点的平衡因子（Balance Factor）。平衡二叉树上所有节点的平衡因子只可能是-1、0或1.如果某一节点的平衡因子绝对值大雨1，则说明此树不是平衡二叉树。**为了方便计算每一个节点的平衡因子我们可以为每个节点赋予height这一属性，表示此节点的高度**

#### insertion in AVL trees 

If an insertion causes T to become unbalanced, we travel up the tree from the newly created node until we find the first node x such that its grandparent z is unbalanced node.

- Since z became unbalanced by an insertion in the subtree rooted at its child y, to rebalance the subtree rooted at z, we must oerform a restructuring
- - we rename x, y, and z to a, b and c based on the order of the nodes in an in-order traversal.
- -z is replaced by b, whose children are now a and c whose chi;dren ,in turn, consist of the four other subtrees formerly children of x, y z. 

##### LL（右旋）

LL的意思是向左子树(L)的左孩子(L)中插入新节点后导致不平衡，这种情况下需要右旋转操作，而不是说LL的意思是右旋，后面的也是一样的。

<img src="https://static01.imgkr.com/temp/60b4e5f170c94b8c9e28f4bc2fba960a.png" alt="WX20210509-214055@2x.png" style="zoom:50%;" />

所谓右旋操作，就是吧上图中的B节点和C节点进行所谓的"父子交换",在仅有的这三个节点的时候，是十分简单的，但是当B节点处存在右子节点的时候，事情就变得复杂了，我们通常的操作是：**抛弃有孩子将其与旋转之后的节点C项链，成为节点C的*左孩子***这样我们就能写出对应的代码。

```java
/**
*源自于https://blog.csdn.net/qq_25343557/article/details/89110319
*/
private Node rightRotate(Node y){
	Node x = y.left;
	Node t3 = x.right;
	x.right = y;
	y.left = t3;
	//更新height
	y.height = Math.max(getHeight(y.left),getHeight(y.right))+1;
	x.height = Math.max(getHeight(x.left),getHeight(x.right))+1;
	return x;
}
```

对应上述代码的图片：

<img src="https://static01.imgkr.com/temp/6823f214496e4d279e9689704975226f.png" alt="WX20210509-214055@2x.png" style="zoom:50%;" />

C

> ```C
> //源自：https://zhuanlan.zhihu.com/p/34899732
> nodeptr_t treeRotateRight(nodeptr_t root) {
>     nodeptr_t left = root->left;
>     
>     root->left = left->right; // 将将要被抛弃的节点连接为旋转后的 root 的左孩子
>     left->right = root; // 调换父子关系
> 
>     left->height = max(treeHeight(left->left), treeHeight(left->right))+1;
>     right->height = max(treeHeight(right->left), treeHeight(right->right))+1;
>     
>     return left;
> }
> ```

##### RR(左旋)

左旋操作和优选操作十分类似，基本是对成的

<img src="https://static01.imgkr.com/temp/e60f6694aa644fdb9c5083167d099e68.png" alt="WX20210509-214055@2x.png" style="zoom:50%;" />

```C
nodeptr_t treeRotateLeft(nodeptr_t root) {
    nodeptr_t right = root->right;

    root->right = right->left;
    right->left = root;

    left->height = max(treeHeight(left->left), treeHeight(left->right))+1;
    right->height = max(treeHeight(right->left), treeHeight(right->right))+1;

    return right;
}
```

```java
/**
 * 左旋转
 */
private Node leftRotate(Node y){
	Node x = y.right;
	Node t2 = x.left;
	x.left = y;
	y.right = t2;
	//更新height
	y.height = Math.max(getHeight(y.left),getHeight(y.right))+1;
	x.height = Math.max(getHeight(x.left),getHeight(x.right))+1;
	return x;
}
```



上述代码对应的图：

<img src="https://static01.imgkr.com/temp/78e339a252304bcdba305f567dd92a09.png" alt="WX20210509-214055@2x.png" style="zoom:50%;" />

##### (LR)



<img src="https://i.loli.net/2021/05/10/XPHOIFh15ZTQopi.png" alt="WX20210510-120358@2x.png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/05/10/adE5lJA8vCFPI7f.png" alt="WX20210510-161156@2x.png" style="zoom:50%;" />

我们需要对上图的y节点进行平衡维护，步骤如上图所示。

##### (RL)

就与LR恰好相反

### (2,4)Tree

A(2,4) tree (also called 2-4 tree or 2-3-4 tree) is a multi-way search with the following properties:

* **Node-Size Property**: every internal node has at most four children
* **Depth Property**: all external nodes have the same depth

Depending on the number of children, an internal node of a (2,4) tree is called a 2-node, 3-node or 4-node.

<img src="https://i.loli.net/2021/05/10/snKcRzlNhVgaY9F.png" alt="WX20210510-161957@2x.png" style="zoom:50%;" />

一个(2,4)树的性质：

* 所有的internal节点最多有4个节点
* 所有的external节点有相同的深度

<img src="https://i.loli.net/2021/05/10/LeXl3ImBAG9rPnO.png" alt="WX20210510-164802@2x.png" style="zoom:33%;" />

上面这张图中10 元素的左边没有连接其他节点，所以它没有连满，也就是说10的左边连接的是一个空节点，哪么这个空节点和15的孩子同样都是空节点，但是祖先的个数却不一样，**所以它就不是2-3-4树**，这种情况会在节点删除的时候发生，所以要做一些调整把它重新调整为2-3-4树。在之后会介绍



#### (2,4)Tree - insertion

当插入的节点中的元素小于三个的时候，直接插就行了，如果插进去的时候发现节点数为4的时候就要重新调整了，将原来三个元素的中间节点提取出来作为父节点。然后剩余元素在作为其子节点（要分裂）。

#### (2,4)Tree - Deletion

<img src="https://i.loli.net/2021/05/10/FYVXmq4hogzruHs.png" alt="WX20210510-171920@2x.png" style="zoom:50%;" />

当进行删除操作的时候，如果都满足2-3-4树的定义的话直接删除就好了。如果删除的时候发现删除后无法满足2-3-4树的定义，就得对树进行调整。

例如上图删除4的时候,就不满足定义了：**all external nodes have the same depth**所以就得调整，首先去找兄弟节点看是否有多余的节点可以弥补，查找后发现有6和8，这里我们选择6,然后将5移下去，保持了叶子节点深度不变。

<img src="https://i.loli.net/2021/05/10/ozcdC4BxlMqYLhu.png" alt="WX20210510-201649@2x.png" style="zoom:50%;" />

这次删除12，12是根节点，所以选择左子树的最右边（也就是前继结点【我乱猜的。。】），11移动走了以后，就需要从父节点中把10移下来保持叶子节点的深度，同时把8和10合并。

<img src="https://i.loli.net/2021/05/10/fNYlsObTrtwCZck.png" alt="WX20210510-202353@2x.png" style="zoom:50%;" />

接下来删除了13，因为依然满足2-3-4树的定义，所以不用调整。

<img src="https://i.loli.net/2021/05/10/YDClJaTNusdXebB.png" alt="WX20210510-202509@2x.png" style="zoom:50%;" />

然后删除了14以后，为了保持叶子节点的深度，继续从父节点向下移动，，但是15的位置却空了，这个空位还需要它的父节点来你不，于是将11移到下面。

<img src="https://i.loli.net/2021/05/10/yc3xNBfEp8qeG1K.png" alt="WX20210510-203854@2x.png" style="zoom:50%;" />

此时15和17的位置显然是不对的，所以将两个节点合并到11的右边。

<img src="https://i.loli.net/2021/05/10/W4Bh3kERUS1H6XI.png" alt="WX20210510-204127@2x.png" style="zoom:50%;" />

然后再将6和11合并为新的根节点

<img src="https://i.loli.net/2021/05/10/hISDGyZtOgXC8nl.png" alt="WX20210510-204133@2x.png" style="zoom:50%;" />







