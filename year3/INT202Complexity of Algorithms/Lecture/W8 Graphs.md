# Graphs(W8)

Connectivity information can be defined by many kinds of relationships that exist between pairs of objects.



For example, connectivity information is present in city maps， where the objects are roads, and also in the routing tables for the internet, where the objects are computers.



Connectivity information is also present in the parent-child relationships defined by a binary tree, where the objects are tree nodes.



Graphs are one way in which connectivity information can be stored, expressed, and utilized.

Connectivity information 可以通过对象之间存在的多种关系来定义。

例如，联通性信息可以表现为城市的地图，对象是道路，也可以是互联网中的路由表，对象是计算机。

联通性信息也可以表示为父亲和孩子之间的关系通过二叉树，其中对象是树的节点。

图可以是存储，表达和利用连接信息的一种方式。

---------------------------

在计算机科学中，一个图就是一些定点的集合，这些订单通过一系列边结对（连接）。定点用圆圈表示，边就是这些圆圈之间的连线。顶点之间通过边连接。

**注意**：顶点有时候也称为节点或者交点，边有时也称为链接。

一个图可以表示一个社交网络，每一个人就是一个顶点，互相认识的人之间通过边连接。

<img src="https://static01.imgkr.com/temp/83d6a71d09334cc9867f5063c681a39f.png" alt="image-20210427214743535.png" style="zoom:50%;" />

图有各种形状和大小。边可以有权重(weight),即每一条边会被非配一个正数或者负数值。老吕一个代表航线的图。各个城市就是顶点，航线就是边，那么边的权重可以是飞行时间，或者机票的价格。

<img src="https://static01.imgkr.com/temp/3d951edfa4034f6286c1d312568fb217.png" alt="image-20210427214743535.png" style="zoom:50%;" />

有了这样一张假设的航线图。从旧金山到莫斯科最便宜的路线是到纽约转机。

边可以是有方向的。在上面提到的例子中，边是没有方向的。例如，如果Ada认识Charles，那么Charles也就认识Ada。相反，有方向的边意味着是单方面的关系。一条从顶点X到顶点Y的边是将X连向Y，而不是将Y连向X

继续前面的航班的例子，从旧金山到阿拉斯加的朱诺有向边意味着从旧金山到朱诺有航班，但是从朱诺到旧金山没有。

<img src="https://static01.imgkr.com/temp/3d8b93a17a2045a99646b0821216a62f.png" alt="image-20210427214743535.png" style="zoom:50%;" />

下面的两种情况也属于图：

<img src="https://static01.imgkr.com/temp/133b452f965c4578ad48d037ea535acd.png" alt="image-20210427214743535.png" style="zoom:50%;" />

左边的是树，右边的是链表。他们都可以被当成是图，只不过是一种更简单额形式。他们都有顶点(节点)和边(连接)。

第一种图包含圈(cycles),即你可以从一个顶点出发，沿着一条路径最终会回到最初的顶点。树不是包含圈的图。

另一种常见的图类型是单向图或者DAG：

<img src="https://static01.imgkr.com/temp/1abce62098b24671bac7c0c488b69ff7.png" alt="image-20210427214743535.png" style="zoom:50%;" />







就像树一样，这个图没有任何圈(无论你从哪一个节点出发,你都无法回到最初的节点)，但是这个图是有向边(通过一个箭头表示，这里的箭头不表示继承关系)。

## 为什么要使用图

例如，假设你有一系列任务需要完成，但是有的任务必须等待其他任务完成后才可以开始。你可以通过非循环有向图来建立模型：

<img src="https://static01.imgkr.com/temp/b01c86af6d124cb097a65ab7dfa1eb22.png" alt="image-20210427214743535.png" style="zoom:50%;" />

每一个顶点代表一个任务。两个任务之间的边表示目的任务必须等到源任务完成后才可以开始。比如，在任务B和任务D都完成之前，任务C不可以开始。在任务A完成之前，任务B和D都不能开始.

现在这个问题就通过图描述清楚了，你可以树用深度优先搜索算法来执行拓扑排序。这样就可以将所有的任务排入最优的执行顺序，保证等待任务完成的时间最小化。(这里可能的顺序之一是A,B,D,E,C,F,G,H,I,J,K)

不管是什么时候遇到困难的编程问题，问一问自己："如何用图来表述这个问题？"图都是用于表示数据之间的关系。诀窍在于如何定义"关系"

如果你是一个音乐家，你可能喜欢这个图：

<img src="https://static01.imgkr.com/temp/86960808110c4856be841efb6c7f0a25.png" alt="image-20210427214743535.png" style="zoom:50%;" />

这些顶点来自C大调的和弦。这些边--表示和弦之间的关系--描述了怎样从一个和弦到另一个和弦。这是一个有向图，所以肩头的方向表示了怎样从一个和弦到下一个和弦。它同时还是一个加权图，每一条边的权重(这里用线条的宽度来表示)说明了两个和弦之间的强弱关系。如你所见，G7-和弦后是一个D和选和一个很轻的Am和弦。

程序员常用的另一个图就是状态机，这里边描述了状态之间的切换的条件。下面这个状态机描述了一个猫的状态：

<img src="https://static01.imgkr.com/temp/4c00fe8b5326494599d29105093b5875.png" alt="image-20210427214743535.png" style="zoom:50%;" />

## 顶点和边

理论上，图就是一对顶点和边对象而已，但是怎么在代码中描述出来呢？

有两种主要的方法：邻接列表和邻接矩阵。

**邻接矩阵**：在邻接矩阵实现中，由行和列都表示顶点，由两个顶点所决定的矩阵对应元素表示这里两个顶点是否相连、如果相连这个值表示的是相连边的权重，例如，如果从顶点A到顶点B有一条权重为5.6的边，那么矩阵中第A行第B列的位置的元素应该是6.5:

<img src="https://static01.imgkr.com/temp/bb14a371b8ec48b6a01c93451f77a5c7.png" alt="image-20210427214743535.png" style="zoom:50%;" />



## Pathfinding algorithms

### Depth First Search(DFS)

Depth First Search(DFS) is a means of exploring a graph.

The basic idea is that we start at some vertex, and start moving away from this start vertex.

We travel "as far as possible" before we have to "back up" because we get to point where we have hit vertices that have all been previously found.

#### Depth First Search Algorithm(recurisive)

> DFS(G,v)
>
> ​	input: A graph G and a vertex v of G.
>
> ​	input: A labeling of the edges of G
>
> ​	**for** all edges e in G.<SUB>INCIDENT</SUB>E<SUB>DGES</SUB>(V)
>
> ​		**do**
>
> ​			**if** UNEXPLORED(e)
>
> ​				**then** w <-- G.<sub>opposite</sub>(v,w)	//Return the endpoint
>
> ​					**if** UNEXPLORED(w)
>
> ​						**then** label e as discovery edge
>
> ​							DFS(G,w)
>
> ​					**else**
>
> ​							Label e as back edge

##### Depth First Search of a Graph

<img src="https://static01.imgkr.com/temp/2034c39a99d84b589aa7d45a49e52989.png" alt="image-20210427214743535.png" style="zoom:50%;" />

##### DepthFirstSearch(G,A)

<img src="https://static01.imgkr.com/temp/8ebc05d80f6a4e8dbada22cea6911313.png" alt="image-20210427214743535.png" style="zoom:50%;" />



​								**Here we add the edge (A,E) to our Depth First Search tree.**

##### DepthFirstSearch(G,E)



<img src="https://static01.imgkr.com/temp/2c69fedd3253473d876b3d34af4f34ab.png" alt="image-20210427214743535.png" style="zoom:50%;" />

​								**Here we add the edge (E,F) to our Depth First Search tree.**

##### DepthFirstSearch(G,F)

<img src="https://static01.imgkr.com/temp/a1dbe608196544b4ada963af45aed812.png" alt="image-20210427214743535.png" style="zoom:50%;" />

​							**Here we add the edge (F,C) to our Depth First Search tree.**

##### DepthFirstSearch(G,C)

<img src="https://static01.imgkr.com/temp/d02755827d54456fb0ec82464e21f3d8.png" alt="image-20210427214743535.png" style="zoom:50%;" />

​							**Here we add the edge (C, D) to our Depth First Searchtree.**

##### DepthFirstSearch(G,D)

<img src="https://static01.imgkr.com/temp/f2411907555e49158d890a0023e65e89.png" alt="image-20210427214743535.png" style="zoom:50%;" />

​							**Here don’t add any edge as the neighbor of D (F) has already been visited. The edge 																	(D, F) is a back edge.**

##### DepthFirstSearch(G,C)

<img src="https://static01.imgkr.com/temp/c0aa6bef1a434744a46a6a713f8652dd.png" alt="image-20210427214743535.png" style="zoom:50%;" />

​							**Here we add the edge (C, B) to our Depth First Searchtree.**

##### DepthFirstSearch(G,B)

<img src="https://static01.imgkr.com/temp/84488ce2d06c49f38e9826cb2c973320.png" alt="image-20210427214743535.png" style="zoom:50%;" />

**Here we don’t add the edge (B, E) to our Depth First Search tree as E has already been visited,so the edge (B, E) is a back edge.**

##### DepthFirstSearch(G,B)

<img src="https://static01.imgkr.com/temp/c4a348ecab4342eb92ffd655d262c860.png" alt="image-20210427214743535.png" style="zoom:50%;" />

**Here we don’t add the edge (B, E) to our Depth First Search tree as E has already been visited,so the edge (B, E) is a back edge.**

##### DepthFirstSearch(G,B)

<img src="https://static01.imgkr.com/temp/6ee42126292a457192e3f0364efdfe71.png" style="zoom:50%;" />

**Here we don’t add the edge (B, A) to our Depth First Search tree as A has already been visited. The edge (B, A) is a back edge.**

##### DepthFirstSearch(G,F)

<img src="https://static01.imgkr.com/temp/31370b060f40457c951f19a10e9084ce.png" style="zoom:50%;" />

**Here we don’t add the edge (F, A) to our Depth First Search tree as A has already been visited. The edge (F, A) is a back edge.**

#### Depth First Search(DFS) Algorithm (non-recurisive)

We can write a non-recurisive version of th eDFS Algorithm.

To control the. Search we use a <mark>stack</mark> data structure. This means that the most recently visited vertex is the from which we continue our search.

>DFS(G,V)
>
>​	Input:A graph G and a vertex v of G
>
>​	Output: A labeling of the discovery and bacl edges of G
>
>​	S.push(v)
>
>​	VISITED(V) <-- TRUE
>
>​	**while** not S.isEmpty()**do**
>
>​		u<--S.top()
>
>​		**if** there is an eddge (u,w) and not VISITED  (w) **then**
>
>​				S.push(w)
>
>​				VISITED(w) <-- true
>
>​				parent(w)<--u
>
>​				Label the edge(u,w) as a discovery edge 
>
>​		**else if** there is an edge(u,w) as a discovery edge
>
>​				Lable the edge(u,w) as a back edge
>
>​		**else**
>
>​				S.pop()



### Breadth First Search(BFS)

Breadth First Search(BFS) is the other common way of exploring a graph.

In contrast to the DFS method, the Breadth First Search algorithm starts at a vertex and first explors the entire neighborhood of that vertex.

So the DFS method generates "long, skinny" search trees, while the BFS method generates "short,bushy" one.

##### Breadth First Search Algorithm

**BFS(G,v)**

> ​	Input: A graph G and a vertex v of G.
>
> ​	Outout: A labeling of the edge of G
>
> Q.enquenue(v)
>
> VISITED(V)<--true
>
> **while** not Q.isEmptyy() **do**
>
> ​		u<-- Q.dequeue()
>
> ​		**for** each edge(u,w) incident to u **do**
>
> ​				**if** not VISITED(w) **then**
>
> ​					Label(u,w) as a discovery edge
>
> ​					VISITED(w)<-- ture
>
> ​					Q.enqueue(w)
>
> ​				**else**
>
> ​					Label(u,w) as a cross edge
>
> ​			
>
> ​				

## DFS vs BFS

DFS traversal:

* Is better for answering complex connectivity questions.
* Produces a spanning tree, such that, all non-tree edges are back edges.
  * Back edge: It is an edge (u,v) such that v is ancestor of node u but not part of DFS tree.

BFS traversal:

* Finds shortest path in a graph.
* Produces a spanning tree, such that, all non-tree edges are cross edges.
  * it is edge witch connects two node such taht they do not have any ancestor and decendant relationship between them.

## Weighted Graphs

## Greedy Apprahch to SSSP(单源最短路径)

## Edge Relaxation

## Fixing the next entry of D

## Dijkstra’s algorithm

## Bellman-Ford Algorithm





​	



















