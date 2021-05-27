# Sorting Algorithmsthm(W6)

## Heap-Souring

* Consider a priority queue with n items implemented by means of a heap
  * ​	the space used is O(n)
  * methods `insertItem` and `removeMin` take O(long n) time
  * methods `size`  ,`isEmpty`,`minKey`, and `minElement` take time O(1) time

* Using a heap-based priority queue, we can sort a sequence of n elements in O(nlog n) time
* The resulting algorithm is called heap-sort
* The resulting algorithm is called heap-sort

## Divide-and-Conquer

The divide-and-conquer method is a means that ca be used to solve some algorithmic problems. This general method consists of the following steps:

* Divide: if the input size is small then solve the problem directly
* Recur: Recurisively solve the sub-problems associated with subsets.
* Conquer: Take the solutions to sub-problems and emerge into a solution to the original problem.

## MergeSort 

Merge-sort on an input sequence S with n elements consists of three steps:

* divide: partition S into two sequences S<sub>1</sub> and S<sub>2</sub> of about n/2 elements eath
* Recur: recursively sort S<sub>1</sub> and S<sub>2</sub> 
* Conquer: mergeS<sub>1</sub>and S<sub>2</sub> into a unique sorted sequence

> Algorithm mergeSort(S,C)
>
> ​	**Input** sequence S with n elements, comparator C
>
> ​	**Output** sequuence S sorted according to C
>
> ​	**if** S.size() > 1
>
> ​		(S<sub>1</sub>,S<sub>2</sub>)  <--- partitions(S,n/2)
>
> ​		mergeSort(S<sub>1</sub>,C)
>
> ​		mergeSort(S<sub>2</sub>,C)
>
> ​		S <-- merge(S<sub>1</sub>,S<sub>2</sub>)

## Master Method

Let a >= 1 and b > 1 be constants, let f(n) be a function， and let T(n) be defined on the nonnegative integers by the recurrence

T(n) = aT(n/b) + f(n).

where we interpret n/b to mean either ⌊n/b⌋ or ⌈n / b⌉. Then T(n) has the following asymptotic bounds:

<img src="https://i.loli.net/2021/05/12/iwYrzxQO2XeEmIR.png" alt="WX20210512-141852@2x.png" style="zoom:50%;" />



<img src="https://i.loli.net/2021/05/12/DQjqaUIoOhHETXn.png" alt="WX20210512-141852@2x.png" style="zoom:50%;" />

**例1**

<img src="https://i.loli.net/2021/05/12/zN6hut5nPTd3G8C.png" alt="WX20210512-143253@2x.png" style="zoom:50%;" />

**例2**

<img src="https://i.loli.net/2021/05/12/OkTIq4iRr7BafZo.png" alt="WX20210512-143703@2x.png" style="zoom:50%;" />

**例3**

<img src="https://i.loli.net/2021/05/12/ERFldT4YyCqmtg2.png" alt="WX20210512-144151@2x.png" style="zoom:50%;" />

**例4**

<img src="https://i.loli.net/2021/05/12/79YP5SZwHklUNVX.png" alt="WX20210512-151019@2x.png" style="zoom:50%;" />

**例5**

<img src="https://i.loli.net/2021/05/12/qdbh2pKyTmEewWY.png" alt="WX20210512-151641@2x.png" style="zoom:50%;" />

## Matrix Multiplication:An example



## Counting inversions: Another example

## Optimization Problems

* Optimization problems can have many possible solutions, and each solution has a value, and we wish to find a solution with the optimal (minimum or maximum) value.
* Algorithms for optimization problems typically go through a sequence of steps, with a set of choices at each step.
* A greedy algorithm is a process that always makes the choice that looks best at the moment. That is, it makea locally optimal choice in the hope that this choice will lead to a globally optimal solution.

### Greedy Method

* A word of warning The greedy approach does not always lead to an optimal solution.
* Problems that have a greedy solution are said to process the  **greedy-choice property**.
* The greedy method is also used for some**hard** (i.e. difficult to solve) problems in order to generate approximate solutions.

#### Interval Scheduling( 贪心区间调度)

#### Greedy Method（The Knapsack Problem)

**题目描述**

有n个物品，他们各自的体积和价值，现在有给定容量的背包，如何让背包里装入的物品具有最大的价值总和？

为了方便讲解和理解，下面讲述的例子均先采用具体的数字带入:即 e g: number = 4,capacti



























