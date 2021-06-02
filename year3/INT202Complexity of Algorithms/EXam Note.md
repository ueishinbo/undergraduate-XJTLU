# EXam Note

## Q1. Complexity

* Consider the following code fragment

  > for i = 1 to n do
  >
  > ​	for j = i to 2 * i do
  >
  > ​		output foobar

  Let T(n) denote the number of times 'foobar' is printed as a function of n.

  1. express T(n) as a summation (actually two nested summations)
  2. Simplify the summation and give the worst-case running time using Big Oh notation

  The processing time of a sorting algorithm is described by the following recurrence equation(c is a positive constant):

  ​	T(n) = 3T(n/3) + 2cn

  ​	T(1) = 0

  1. Solve this equation to derive an explicit formula for T(n) assuming n = 3m and specify the Big-Oh complexitly of the algorithm
  2. Find out where the above algorithm is faster or slower than usual Mergesort that splits recursively an array into two subarrays and then merges the souted subarrays in linear time cn.

  解：

  

  

##  Q2. Sorting and Complexity

可能会让你画一个AVL树，插入和删除都要考虑子节点的平衡

https://blog.csdn.net/Demon_LMMan/article/details/114835679

平衡二叉树和堆的区别：**logic structure:** heap is a complete bianry tree, it don't care about which children is smaller, it just need guarantee the root is the bigget/smallest one. but binary search tree need the left child node is smaller and the right child node is bigger. **store structure**: heap is a array, it has index, can use id to access the node, by this way, saving the space complexity. but bianry search tree is the Linked structure. the parent pointer point the child address.

让你根据前序遍历和后续遍历画出二叉树

堆的时间复杂度是nlogn

对对任何的操作的时间复杂度都是logn

AVL树的任何操作时间复杂度都是logn

## Q3. Searching, Complexity and Pseudo-code



## Q4. Dynamic Programming



## Q5. Flow Network



## Q6. Graph

adjacency matrix:邻接矩阵，就是把有向图

## Q7. Cryptography

## Q8. NP Completeness

